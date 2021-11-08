<template>
    <div class="h-screen mx-auto bg-pink-50 textured grid place-items-center">
        <div class="bg-blue-200 mt-auto mb-auto px-10 pt-10 pb-5 border-4 max-w-2xl border-blue-400">
            <h1 class="font-serif text-blue-600 text-6xl">
                tadhg boyle <img :src="me" alt="Me!" class="max-h-32 float-right inline">
            </h1>
            <h5 class="font-mono text-blue-500 text-2xl pt-3 pb-5">
                web developer
                <br>
                software engineer
            </h5>
            <div class="font-serif text-blue-500 pb-5 space-y-4">
                <p>
                    <span class="text-xl pr-2">👋</span>hey! i'm tadhg, a CS student at BCIT & developer based in vancouver.
                </p>
                <p>
                    for the last 5 years i've been developing my skills as a programmer by working on many open source projects and pairing with clients to create awesome products.
                </p>
                <p>
                    i offer full stack web and java development services.
                </p>
                <p>
                    interested? let's chat!
                    <br>
                    discord: <a href="https://discord.com/users/271510274475819008"><span class="font-bold">aberdeener#0001</span></a>
                    <br>
                    email: <a :href="'mailto:' + email"><span class="font-bold">{{ email }}</span></a>
                </p>
            </div>
            <div class="text-purple-500 flex justify-center gap-x-6">
                <a href="https://github.com/Aberdeener" target="_blank">🖥️ <span class="hover:underline">github</span></a>
                <a href="https://www.linkedin.com/in/tadhg-boyle/" target="_blank">💭 <span class="hover:underline">linkedin</span></a>
                <a href="https://twitter.com/Aberd33n3r" target="_blank">🐦 <span class="hover:underline">twitter</span></a>
            </div>
        </div>
    </div>
</template>

<script>
import me from '/me.png';

export default {
    data() {
        return {
            email: 'meATghdatDOTsh'
                    .replace('AT', '@')
                    .replace('ghdat', 'tadhg')
                    .replace('DOT', '.'),
            me: me,
        }
    }
}
</script>

<style>
.textured {
    background-image: url("data:image/svg+xml,%3Csvg width='40' height='40' viewBox='0 0 40 40' xmlns='http://www.w3.org/2000/svg'%3E%3Cg fill='%23BFDBFE' fill-opacity='1' fill-rule='evenodd'%3E%3Cpath d='M0 40L40 0H20L0 20M40 40V20L20 40'/%3E%3C/g%3E%3C/svg%3E");
}
</style>
