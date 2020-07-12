<template>
    <div id="All-friends">
      <h2>All Friends</h2>
      <!-- 希望給each friend一個unique，這邊採用index     -->
      <div v-for="(friend, index) in friends" :key="index">
        <!-- span是inline元素，用法類似於div(區塊元素) -->
        <!-- 這套件真的很屌，他可以知道當前這個friend.name，雖然他是以iterable方式產生的 -->
        <span @click="unfriend(friend.name)">{{ friend.name }}</span>
      </div>
    </div>
</template>

<script>
    export default {
        name: "AllFriends",
        // 除此之外還要於component裡面新增props: []這個array attr/property，來告知要將這個attr置入prop
        // array之中允許有多個prop，可允許multiple props，是寫你的localName進來
        props: ['friends'],
        data() {
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
        },
        methods: {
          // js的obj是長成{}，以花括號包覆
          // ES6語法 name:name可以省略成name，就會自動將二者對應(名字一樣的前提)
          unfriend(name){
              // 透過emit method來將custom event從child component傳給parent component
              // 正確來說$emit可以觸發父元件的，emit可將custom event給parent
              // 會叫做custom是因為可以帶一些訊息、動作，譬如這邊，是將點擊的friend.name隨click送回去

              // $emit需要兩個參數，第一個是這個事件的名稱(自定義，因此叫做custom)
              // 事件建立後就可以做監聽EX: 這邊第一個參數是此custom eventName，@delete
              // 第二個參數則是optional，any data you want to send with this custom event
              // ES6語法 name:name可以省略成name，就會自動將二者對應(名字一樣的前提)
              // 這組data obj只有一個name:name，其實他允許多個
              this.$emit('delete', {name})
          }
        }
    }
</script>

<style scoped>

</style>
