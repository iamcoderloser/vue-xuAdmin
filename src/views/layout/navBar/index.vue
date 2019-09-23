<template>
    <div>
        <el-header id="header">
            <span class="hideAside" @click="collapse"><i class="fa fa-indent fa-lg"></i></span>
            <ul class="personal">
                <li class="fullScreen" @click="fullScreen">
                <el-tooltip class="item" effect="dark" content="全屏" placement="bottom"><i
                    class="fa fa-arrows-alt fa-lg"></i></el-tooltip>
                </li>
                <li>
                <langSelect></langSelect>
                </li>
                <li>{{ $t(`role.${this.$store.getters.info.role}`) }}</li>
                <li>
                <el-dropdown @command="handleCommand">
                        <span class="el-dropdown-link">
                            夏洛克丶旭<i class="el-icon-arrow-down el-icon--right"></i>
                        </span>
                    <el-dropdown-menu slot="dropdown">
                    <el-dropdown-item command="a">{{ $t('userDropdownMenu.basicInfor') }}</el-dropdown-item>
                    <el-dropdown-item command="b">{{ $t('userDropdownMenu.changePassword') }}</el-dropdown-item>
                    <el-dropdown-item command="logout" divided>{{ $t('userDropdownMenu.logout') }}</el-dropdown-item>
                    </el-dropdown-menu>
                </el-dropdown>
                </li>
                <li class="icon"><img :src="avatar"/></li>
            </ul>
        </el-header>

        <el-menu
            :default-active="activeIndex"
            class="el-menu-demo"
            mode="horizontal"
            @select="handleSelect"
            background-color="#333"
            text-color="#fff"
            active-text-color="#ffd04b">
            <template   v-for="(menuItem , index) in menuItems" >
              <el-menu-item :index="(menuItemIndex++)+''" v-if="!menuItem.hidden" :key="index">{{ $t(`routeNmae.${menuItem.name}`)}}</el-menu-item>
            </template>
            
        </el-menu>
    </div>
</template>

<script>
  import Cookies from 'js-cookie'
  import langSelect from '../../../components/lang/langSelect'

  export default {
    name: 'NavBar',
    components: {langSelect},
    data () {
      return {
        isfullScreen: true,
        avatar: './static/images/icon.jpg',  
        activeIndex:'1',
        menuItemIndex:1
      }
    },
    computed:{
      menuItems() {
        var routers = this.$store.getters.routers
        debugger
        return routers
      }
    },
    methods: {
      select(){},
      handleSelect() {},
      collapse () {
        this.$store.dispatch('collapse')
      },
      fullScreen () {
        if (this.isfullScreen) {
          var docElm = document.documentElement
          if (docElm.requestFullscreen) {
            docElm.requestFullscreen()
          } else if (docElm.mozRequestFullScreen) {
            docElm.mozRequestFullScreen()
          } else if (docElm.webkitRequestFullScreen) {
            docElm.webkitRequestFullScreen()
          } else if (elem.msRequestFullscreen) {
            elem.msRequestFullscreen()
          }
          this.isfullScreen = false
        } else {
          if (document.exitFullscreen) {
            document.exitFullscreen()
          } else if (document.mozCancelFullScreen) {
            document.mozCancelFullScreen()
          } else if (document.webkitCancelFullScreen) {
            document.webkitCancelFullScreen()
          } else if (document.msExitFullscreen) {
            document.msExitFullscreen()
          }
          this.isfullScreen = true
        }
      },
      handleCommand (command) {
        if (command === 'logout') {
          Cookies.remove('token');
          location.reload()

        }
      }
    }
  }
</script>

<style scoped>
    .el-menu.el-menu--horizontal {

        border-bottom: none;

    }
</style>

<style lang="scss">
  $top: top;
  $bottom: bottom;
  $left: left;
  $right: right;
  $leftright: ($left, $right);
  %w100 {
    width: 100%;
  }

  %h100 {
    height: 100%;
  }

  %cursor {
    cursor: pointer;
  }

  html, body, #app, .el-container, #asideNav, ul.el-menu {
    @extend %h100;
  }

  @mixin set-value($side, $value) {
    @each $prop in $leftright {
      #{$side}-#{$prop}: $value;
    }
  }

  #header {
    max-height: 50px;
    line-height: 50px;
    box-shadow: 0 1px 2px 0 rgba(0, 0, 0, .05);
    display: flex;
    justify-content: space-between;
    .hideAside {
      @extend %cursor;
    }
    .personal {
      display: flex;
      flex-direction: row;
      li {
        @include set-value(margin, 13px);
        font-size: 12px;
      }
      .fullScreen {
        @extend %cursor;
      }
      .el-dropdown-link {
        @extend %cursor;
      }
      .icon img {
        margin-#{$top}: 7px;
        -webkit-border-radius: 5px;
        -moz-border-radius: 5px;
        border-radius: 5px;
        width: 40px;
        height: 40px;
      }
    }
  }
</style>