<template>
  <div id="app">
    <h1>{{ title }}</h1>
    <!--
           不會受到Navbar的style標籤影響，因為有<style scoped>
           後來是改以在css selector於選擇上增加獨特性來避免影響到跨components
    <nav>
      <h2>Menu from App.vue</h2>
      <ul>
        <li><a href="">Home</a></li>
        <li><a href="">About</a></li>
        <li><a href="">Contact</a></li>
      </ul>
    </nav>
    -->
    <Navbar />
    <!-- 若希望sending某data properties至other components需要data binding在下面任務中(不知可否理解成instance)
         他又叫他dynamically bind data，會幫他取一個localName
         通常為了一致性consistent會取名一樣
         "!!這種父子組件溝通的方式叫做 props !! Passing down props or props your attribute/properties !!"
         形式
              <componentName :LocalName="attrName"/>
         除此之外還要於component裡面新增props: []這個array attr/property，來告知要將這個attr置入prop
         array之中允許有多個prop，可允許multiple props，是寫你的localName進來
     -->
    <!--  emit將事件送回來，然後這邊@delete去監聽，並且react去做deleteFriend() method  -->
    <AllFriends :friends="friends" @delete="deleteFriend"/>
    <OnlineFriends :friends="friends"/>
    <!--
          這是沒有colon冒號，意思是沒有data-binding，表示props是一個一般string variable
          不會對應到root component的property/attribute，只會渲染到friends的字串
          <OnlineFriends friends="friends"/>
    -->
  </div>
</template>

<script>
  // from xxx.vue可以省略副檔名filename extension
  // 由於是以export default來匯出，因此他是沒有要求名稱的
  // 只是習慣上會傾向跟.vue一樣，來匯入至root component之中
  //import Navbar from "./Navbar"，vue中的script可以省略;
  import Navbar from "./Navbar"
  import AllFriends from "./AllFriends"
  import OnlineFriends from "./OnlineFriends"
  export default {
    // 雖然如下面所提，傾向一樣，這邊叫做app卻也有種instance與class的區別感
    name: 'app',
    components: {OnlineFriends, AllFriends, Navbar},
    //components: {Navbar},
    // 引入進來的component要註冊register到這個root component下
    // components可以在不同之間之下去註冊
    comments:{
      // 得幫他取一個local name，一般來說the same維持一致性
      // Navbar: Navbar
      // 名字一樣的話可以打成下面形式，因此建議同樣
      Navbar,
      AllFriends,
      OnlineFriends
    },
    data () {
      return {
        title: 'Welcome to Your Vue.js App',
        // friends放在這邊是比較合理的，因為AllFriends、OnlineFriends都會共用到此data
        friends: [
          {name: 'Mario', online: true},
          {name: 'Luigi', online: false},
          {name: 'Toad', online: true},
          {name: 'Bowser', online: false}
        ]
      }
    },
    methods:{
      // 因為這個事件有帶參數，因此需要一個parameter來承接
      // 慣例上會叫做payload，但其實並沒有限制說一定要叫什麼
      deleteFriend(payload){
        // 這條只是測試看看，是否有抓到點下去的那個內容的content
        // 要注意這個從child帶回來的實際上{}物件，若要真的拿出值要dot and key
        // 否則會是{...}格式，也無法做boolean、compare比較
        console.log(payload.name)
        // 這明顯要用filter return結果蓋掉當前當前的friend data obj
        // 參數 => { ... }，這是ES6風格的function，針對each friend與帶進來參數比較作回傳
        // filter是針對回傳的True與False結果來斷定是否要保留那條資料
        this.friends = this.friends.filter(friend => {
            // 不等於的要TRUE保留下來
            return friend.name !== payload.name
        })

      }
    }
  }
</script>

<!-- 要注意引入的component會受到root component的style給影響 -->
<style>
h1{
  color:#444;
  font-weight: normal;
  /* h2 這個block element中的文字會置中 */
  text-align: center;
}
</style>
