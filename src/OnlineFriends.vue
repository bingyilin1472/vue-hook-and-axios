<template>
    <div id="online-friends">
      <h2>Online Friends</h2>
      <div v-for="(friend, index) in friends" :key="index">
        <!-- span是inline元素，用法類似於div(區塊元素) -->
        <span v-if="friend.online">{{ friend.name }}</span>
      </div>
    </div>
</template>

<script>
    export default {
        name: "OnlineFriends",
        // 除此之外還要於component裡面新增props: []這個array attr/property，來告知要將這個attr置入prop
        // array之中允許有多個prop，可允許multiple props，是寫你的localName進來
        props: ['friends'],
        data(){
          return{
            // 回傳一個friends物件(array)，其中each friend也會是一個obj(並有name、online status)
            // AllFriends跟OnlineFriends都採用這個Array，因此這樣會有一致性問題(移到root component)合理
            // 同時每次更新僅用update it once in one place(一次更新/一個地方)< good design
            // friends: [
            //   {name: 'Mario', online: true},
            //   {name: 'Luigi', online: false},
            //   {name: 'Toad', online: true},
            //   {name: 'Bowser', online: false}
            // ]
          }
        }
    }
</script>

<style scoped>

</style>
