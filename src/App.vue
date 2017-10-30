<template>
    <v-app light>
        <v-toolbar fixed app :clipped-left="clipped">
            <v-toolbar-title v-text="title"></v-toolbar-title>
            <v-spacer></v-spacer>
            <v-tooltip bottom>
                <v-btn
                        icon
                        slot="activator"
                        :href="author_blog_url">
                    <v-icon>mdi-web</v-icon>
                </v-btn>
                <span>Enter my blog</span>
            </v-tooltip>
            <v-tooltip bottom>
                <v-btn
                        icon
                        slot="activator"
                        @click.stop="rightDrawer = !rightDrawer">
                    <v-icon>people</v-icon>
                </v-btn>
                <span>Friends link</span>
            </v-tooltip>
        </v-toolbar>
        <main>
            <v-content>
                <v-container fluid grid-list-md>
                    <v-slide-y-transition mode="out-in">
                        <v-layout row wrap my-4>
                            <!-- Left card -->
                            <v-flex d-flex xs12 sm4 offset-sm1>
                                <v-card id="left_card">
                                    <v-layout column align-center my-4 mx-3>
                                        <v-tooltip bottom>
                                            <v-avatar size="64" slot="activator">
                                                <img :src="author_avatar.url"
                                                     style="height: 128px; width: 128px;" alt="">
                                            </v-avatar>
                                            <span v-text="author_avatar.alt"></span>
                                        </v-tooltip>
                                        <v-layout mt-4 column align-center id="author_name">
                                            <p v-text="author" class="headline"></p>
                                        </v-layout>
                                        <div class="text-xs-center" id="tags_container">
                                            <v-chip
                                                    v-for="(item, i) in author_tags"
                                                    :key="i"
                                                    :color="item.color"
                                                    text-color="white">
                                                <v-avatar :class="item.color + ' darken-2'">
                                                    <v-icon>{{ item.icon_id }}</v-icon>
                                                </v-avatar>
                                                {{ item.name }}
                                            </v-chip>
                                        </div>
                                    </v-layout>
                                    <v-divider></v-divider>
                                    <v-layout mx-4 my-4 class="title">
                                        短期寻求广告位合作伙伴……
                                        <br>等我想好写什么就去掉了
                                    </v-layout>
                                </v-card>
                            </v-flex>
                            <!-- Right card -->
                            <v-flex d-flex xs12 sm6>
                                <v-card id="right_card">
                                    <v-list two-line>
                                        <v-subheader inset>My information</v-subheader>
                                        <template v-for="(item, i) in author_infos">
                                            <v-list-tile avatar>
                                                <v-list-tile-avatar>
                                                    <v-icon medium>{{ item.icon_id }}</v-icon>
                                                </v-list-tile-avatar>

                                                <v-list-tile-content>
                                                    <v-list-tile-title v-text="item.title">
                                                    </v-list-tile-title>
                                                    <v-list-tile-sub-title v-text="item.info">
                                                    </v-list-tile-sub-title>
                                                </v-list-tile-content>
                                            </v-list-tile>

                                            <v-divider
                                                    inset
                                                    v-if="i + 1 < author_infos.length"
                                            ></v-divider>
                                        </template>
                                        <v-subheader inset>Contact me</v-subheader>
                                        <template v-for="(item, i) in contact_methods">
                                            <v-list-tile avatar :href="item.url">
                                                <v-list-tile-avatar>
                                                    <v-icon medium>{{ item.icon_id }}</v-icon>
                                                </v-list-tile-avatar>

                                                <v-list-tile-content>
                                                    <v-list-tile-title v-text="item.title">
                                                    </v-list-tile-title>
                                                    <v-list-tile-sub-title v-text="item.id_name">
                                                    </v-list-tile-sub-title>
                                                </v-list-tile-content>
                                            </v-list-tile>

                                            <v-divider
                                                    inset
                                                    v-if="i + 1 < contact_methods.length"
                                            ></v-divider>
                                        </template>
                                    </v-list>
                                </v-card>
                            </v-flex>
                        </v-layout>
                    </v-slide-y-transition>
                </v-container>
            </v-content>
        </main>
        <v-navigation-drawer
                temporary
                right
                v-model="rightDrawer"
                app
        >
            <v-list>
                <v-list-tile v-for="(item, i) in friend_links" :key="i" :href="item.url">
                    <v-list-tile-action>
                        <v-icon light>link</v-icon>
                    </v-list-tile-action>
                    <v-list-tile-title v-text="item.title"></v-list-tile-title>
                </v-list-tile>
            </v-list>
        </v-navigation-drawer>
        <v-footer :fixed="fixed" app>
            <span>Fork me on <a href="https://github.com/fython/about-me-page">GitHub</a></span>
        </v-footer>
    </v-app>
</template>

<script>
    export default {
        data () {
            return {
                clipped: false,
                fixed: false,
                friend_links: [
                    { title: 'Rabi.coffee', url: 'https://1cup.rabi.coffee', tips: '一杯兔子咖啡' },
                    { title: 'Rikka 的博客', url: 'https://shizuku.moe/', tips: '坏耶！是 Rikka' },
                    { title: '千千的博客', url: 'https://wwyqianqian.github.io/', tips: '是 千哥！（' },
                    { title: 'PeterCxy 的博客', url: 'https://typeblog.net/', tips: '彼得蔡的博客' },
                    { title: 'Touko\'s diary', url: 'https://touko.moe/', tips: '橙子大佬的博客' },
                    { title: '祈星辰的博客', url: 'https://loli.xing.moe/', tips: '' },
                    { title: '天宇的博客', url: 'https://www.xdty.org/', tips: '' }
                ],
                rightDrawer: false,
                title: 'About me',
                author: '烧饼 @fython',
                author_blog_url: 'https://feng.moe',
                author_avatar: {
                    url: '/public/avatar.jpg',
                    alt: '来自《此花亭绮谭》，非常治愈的日常番'
                },
                author_tags: [
                    { icon_id: 'mdi-android-head', name: 'Android Dev', color: 'green'},
                    { icon_id: 'mdi-android-studio', name: 'Material Design', color: 'indigo'},
                    { icon_id: 'gamepad', name: 'ACGer', color: 'red'},
                    { icon_id: 'school', name: 'Student', color: 'orange'},
                    { icon_id: 'mdi-windows', name: 'Windows User', color: 'blue'}
                ],
                author_infos: [
                    {
                        icon_id: 'mdi-city',
                        title: '居住地 Location',
                        info: 'Guangdong, China'
                    },
                    {
                        icon_id: 'translate',
                        title: '语言 Language',
                        info: 'Chinese (Mandarin & Cantonese)'
                    },
                    {
                        icon_id: 'mdi-tag-heart',
                        title: '最喜欢的文化 Favourite culture',
                        info: 'Cantonese food & Japanese Anime'
                    }
                ],
                contact_methods: [
                    {
                        icon_id: 'mdi-github-circle',
                        title: 'GitHub',
                        id_name: '@fython',
                        url: 'https://github.com/fython'
                    },
                    {
                        icon_id: 'fa-weibo',
                        title: 'Sina Weibo',
                        id_name: '@FungGo',
                        url: 'https://weibo.com/fython'
                    },
                    {
                        icon_id: 'fa-twitter',
                        title: 'Twitter',
                        id_name: '@fython',
                        url: 'https://twitter.com/fython'
                    },
                    {
                        icon_id: 'fa-telegram',
                        title: 'Telegram',
                        id_name: '@fython',
                        url: 'https://t.me/fython'
                    },
                    {
                        icon_id: 'fa-steam',
                        title: 'Steam',
                        id_name: '燒餅',
                        url: 'http://steamcommunity.com/id/fython'
                    },
                    {
                        icon_id: 'fa-wheelchair-alt',
                        title: 'osu!',
                        id_name: 'fythonx',
                        url: 'https://osu.ppy.sh/users/2116530'
                    }
                ]
            }
        }
    }
</script>