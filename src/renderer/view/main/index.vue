<template>
    <div>
        <Layout>
            <Header class="header">
                <Menu mode="horizontal" active-name="1" theme="light"
                      style="height: 80px;background-color: #EEF0F6;padding-top: 5px;">
                    <div class="layout-logo"></div>
                    <div class="layout-nav">
                        <MenuItem name="1" :to="{name:'index'}" style="-webkit-app-region: no-drag;">我的网盘</MenuItem>
                        <MenuItem name="2" :to="{name:'listIndex'}" style="-webkit-app-region: no-drag;">传输列表</MenuItem>
                        <MenuItem name="3" style="-webkit-app-region: no-drag;">好友分享</MenuItem>
                        <MenuItem name="4" style="-webkit-app-region: no-drag;">功能宝箱</MenuItem>
                    </div>
                    <div class="right">
                        <span @click="appSetting"><Icon type="ios-settings-outline"/></span>
                        <span v-if="maximum" @click="restoreWindow"><Icon type="ios-contract"/></span>
                        <span v-else @click="restoreWindow"><Icon type="ios-expand"/></span>
                        <span @click="minWindow"><Icon type="md-remove"/></span>
                        <span @click="exitApp"><Icon type="md-close"/></span>
                    </div>
                </Menu>
            </Header>
            <Layout style="margin-top: 16px;-webkit-user-select: none;">
                <Sider width="165" style="background-color: #FFFFFF;">
                    <router-view name="menu" :menuHeight="100"/>
                </Sider>
                <Layout style="background-color: #FFFFFF;">
                    <Content :style="{background: '#fff'}">
                        <router-view name="main"/>
                    </Content>
                </Layout>
            </Layout>
        </Layout>
        <Update></Update>
    </div>
</template>

<script>

    import Update from "@/components/update";

    export default {
        name: "index",
        components: {Update},
        data() {
            return {
                maximum: false,
            }
        },
        methods: {
            appSetting() {
                this.$electron.ipcRenderer.send('setting');
            },
            exitApp() {
                this.$electron.ipcRenderer.send('exitApp');
            },
            minWindow() {
                this.$electron.ipcRenderer.send('minWindow');
            },
            restoreWindow() {
                this.$electron.ipcRenderer.send('maximizeWindow');
            },
        }
    }
</script>

<style scoped>
    .header {
        -webkit-app-region: drag;
        padding: 0;
        background-color: red;
        -webkit-user-select: none;
    }

    .layout-logo {
        width: 150px;
        height: 30px;
        background: url("../../assets/img/logo.png") no-repeat;
        background-size: 118px;
        border-radius: 3px;
        float: left;
        position: relative;
        top: 15px;
        left: 10px;
        margin-right: 20px;
    }

    .layout-nav {
        -webkit-app-region: no-drag;
        width: 400px;

        float: left;
    }

    .right {
        float: right;
        margin-right: 10px;
        font-size: 20px;
        -webkit-app-region: no-drag;
    }

    .right span {
        cursor: pointer;
        margin: 0 5px;
    }

    .right span:hover {
        color: #E4393c;
    }

</style>
