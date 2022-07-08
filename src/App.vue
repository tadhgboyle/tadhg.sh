<template>
    <div class="h-screen mx-auto bg-pink-50 grid place-items-center" :class="this.backgroundClass">
        <div class="bg-blue-200 mt-auto mb-auto px-10 pt-10 pb-5 border-4 max-w-2xl border-blue-400">
            <h1 class="font-serif text-blue-600 text-6xl">
                tadhg boyle
            </h1>
            <div class="font-serif text-blue-500 pb-5 space-y-4 pt-4">
                <p>
                    <span class="text-xl pr-2">👋</span>hey! i'm tadhg, a CS student & software developer based in edmonton.
                </p>
                <p>
                    for the last 5 years i've been developing my skills as a programmer by working on many open source projects and pairing with clients to create awesome products.
                </p>
                <p>
                    i'm currently interning at Shopify as a backend software developer, where i'm working on the merchant services billing team.
                </p>
                <p>
                    discord: <a href="https://discord.com/users/271510274475819008"><span class="font-bold">aberdeener#0001</span></a>
                    <br>
                    email: <a href="mailto:me@tadhg.sh"><span class="font-bold">me@tadhg.sh</span></a>
                </p>
                <p v-html="nowPlaying"></p>
            </div>
            <div class="text-purple-500 flex justify-center gap-x-6">
                <a href="https://github.com/Aberdeener" target="_blank">🖥️ <span class="hover:underline">github</span></a>
                <a href="https://www.linkedin.com/in/tadhg-boyle/" target="_blank">💭 <span class="hover:underline">linkedin</span></a>
                <a href="https://twitter.com/Aberd33n3r" target="_blank">🐦 <span class="hover:underline">twitter</span></a>
            </div>
        </div>
    </div>
</template>

<style>
.background-textured {
    background-image: url("data:image/svg+xml,%3Csvg width='40' height='40' viewBox='0 0 40 40' xmlns='http://www.w3.org/2000/svg'%3E%3Cg fill='%23BFDBFE' fill-opacity='1' fill-rule='evenodd'%3E%3Cpath d='M0 40L40 0H20L0 20M40 40V20L20 40'/%3E%3C/g%3E%3C/svg%3E");
}

.background-bentley {
    background-image: url("https://bentley.tadhg.sh/-2.gif");
}
</style>

<script>
import axios from 'axios';
import convertXML from 'simple-xml-to-json';
import he from 'he';

export default {
    mounted() {
        this.getLatestSong();
        setInterval(() => {
            this.getLatestSong();
        }, 4000);
    },
    computed: {
        backgroundClass() {
            const date = new Date();
            if (date.getMonth() === 11 && date.getDate() === 23) {
                console.log('🐱 Happy Birthday, Bentley!');
                return 'background-bentley';
            }
            return 'background-textured';
        },
    },
    methods: {
        async getLatestSong() {
            const response = await axios.get('https://ws.audioscrobbler.com/2.0/?method=user.getrecenttracks&user=tadhg-boyle&limit=1&api_key=2866efed3e2acc2afee1a8cc82077046', {
                responseType: 'text',
            });

            const data = convertXML.convertXML(response.data);
            const latestTrack = data.lfm.children[0].recenttracks.children[0].track;

            let text = '🎶 ';
            const nowPlaying = latestTrack.nowplaying;

            if (nowPlaying) {
                text += "i'm currently listening to: ";
            } else {
                text += "i last listened to: ";
            }

            const artist = latestTrack.children[0].artist.content.toLowerCase();
            const title = he.unescape(latestTrack.children[1].name.content).toLowerCase();
            const url = latestTrack.children[5].url.content;

            text += `<a class="hover:underline" target="_blank" href="${url}"><i>${artist} - ${title}</i></a> `;

            let showTime = true;
            if (!nowPlaying) {
                const date = new Date(0);
                date.setUTCSeconds(latestTrack.children[10].date.uts)
                let time = date.toLocaleTimeString([], {
                    hour: 'numeric',
                    minute:'2-digit'
                });
                // some locale date time strings don't end with a period
                if (time.endsWith('.')) {
                    time = time.slice(0, -1);
                }

                const yesterday = new Date();
                yesterday.setDate(yesterday.getDate() - 1);
                if (new Date().toLocaleDateString() !== date.toLocaleDateString()) {
                    if (date.toLocaleDateString() === yesterday.toLocaleDateString()) {
                        text += `yesterday `;
                    } else {
                        showTime = false;
                        text += `a while ago `;
                    }
                }
                if (showTime) {
                    text += `@ ${time}`;
                }
            }

            this.nowPlaying = text;
        }
    }
}
</script>

