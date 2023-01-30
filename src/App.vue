<template>
  <div class="main" @click="closeDiv(); closeErrorDiv()">
    <div class="updiv">
      <div class="test"></div>
      <div class="container">
        <div class="inputdiv">
          <input type="text" class="input" v-model="gameinput" @keydown="openDiv() ; searchGame()">
        </div>
        <div class="errordiv" v-if="openederrordiv&&gameinput.length >= 3"><h2>{{ notfind }}</h2></div>
        <div class="recommendedgamesdiv" v-if="openedgamediv">
          <div class="imageside">
            <li class="liimage" v-for:="img in imagelist" @click="searchedimageOpen(img)"><img :src="img" alt="" class="image"></li>
          </div>
          <div class="nameside">
            <li class="liname" v-for:="game in filteredlist" @click="searchedGameOpen(game)"><button class="namebtn">{{ game }}</button></li>
          </div>
        </div>
      </div>
    </div>
    <div class="downdiv">
      <div class="containerdown">
        <div class="gamenamediv">
          <h1>{{ gamename }}</h1>
        </div>
        <div class="releasedatediv">
          <p class="releasedate">({{ gamereleasedate }})</p>
        </div>
        <div class="imganddesc">
          <img :src="gameimage" class="showimg">
          <div class="descandprice">
            <div class="sdescdiv">
              <p class="showdesc">{{ gamedescription }}</p>
            </div>
            <div class="pricediv">
              <div class="price">
                <h3 class="pricetext">{{ gameprice }}</h3>
              </div>
            </div>
          </div>
        </div>
        <div class="infoandlink">
          <div class="maininfos">
              <div class="infodiv"><h4 class="info">Developer :</h4><h4 class="developer dprr">{{ gamedeveloper }}</h4></div>
              <div class="infodiv"><h4 class="info">Publisher :</h4><h4 class="publisher dprr">{{ gamepublisher }}</h4></div>
              <div class="infodiv"><h4 class="info">Review Count :</h4><h4 class="reviewcount dprr">{{ gamereviewcount }}</h4></div>
              <div class="infodiv"><h4 class="info">Reviews :</h4><h4 class="reviews dprr">{{ gamereviews }}</h4></div>
          </div>
          <div class="link">
            <a :href="gamelink" target="_blank"><button class="steambtn" title="Go to steam page :)"><i class="fa-brands fa-steam"></i></button></a>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import gamelist from "@/assets/games.json"

export default {
  data(){
    return{
      openedgamediv: false,
      openederrordiv: false,

      filteredlist: [],
      imagelist: [],
      
      gameinput: '',
      gamelist: gamelist,
      
      gamename: 'Red Dead Redemption 2',
      gamedescription: 'Winner of over 175 Game of the Year Awards and recipient of over 250 perfect scores, RDR2 is the epic tale of outlaw Arthur Morgan and the infamous Van der Linde gang, on the run across America at the dawn of the modern age.',
      gameimage: 'https://cdn.cloudflare.steamstatic.com/steam/apps/1174180/header.jpg?t=1618851907',
      gameprice: '40,19\u20ac',
      gamereleasedate: '5 Dec, 2019',
      gamedeveloper: 'Rockstar Games',
      gamepublisher: 'Rockstar Games',
      gamereviewcount: '181420',
      gamereviews: '93%',
      gamelink: 'https://store.steampowered.com/app/1174180/Red_Dead_Redemption_2/?snr=1_7_7_230_150_240',
      
      notfind: 'Game not found :(',
    };
  },
  methods: {
    openDiv(){
      if(this.gameinput.length >= 3){
        this.openedgamediv = true;
      }else{
        this.openedgamediv = false;
      }
    },
    closeDiv(){
      if(this.openedgamediv){
        this.openedgamediv = false;
      }
    },
    closeErrorDiv(){
      if(this.openederrordiv){
        this.openederrordiv = false;
      }
    },
    searchedimageOpen(img){
      for (var i = 0; i < this.gamelist.length+1; i += 1){
        if(this.gamelist[i].image == img){

          this.gamename = gamelist[i].name;
          this.gameimage = gamelist[i].image;
          this.gamedescription = gamelist[i].description;
          this.gameprice = gamelist[i].price;
          this.gamereleasedate = gamelist[i].releaseData;
          this.gamedeveloper = gamelist[i].developer;
          this.gamepublisher = gamelist[i].publisher;
          this.gamereviewcount = gamelist[i].reviewCount;
          this.gamereviews = gamelist[i].reviews;
          this.gamelink = gamelist[i].link;

          this.gameinput = '';
          this.filteredlist = [];
          this.imagelist = [];
        }
      }
    },
    searchedGameOpen(game){
      for (var i = 0; i < this.gamelist.length+1; i += 1){
        if(this.gamelist[i].name == game){

          this.gamename = gamelist[i].name;
          this.gameimage = gamelist[i].image;
          this.gamedescription = gamelist[i].description;
          this.gameprice = gamelist[i].price;
          this.gamereleasedate = gamelist[i].releaseData;
          this.gamedeveloper = gamelist[i].developer;
          this.gamepublisher = gamelist[i].publisher;
          this.gamereviewcount = gamelist[i].reviewCount;
          this.gamereviews = gamelist[i].reviews;
          this.gamelink = gamelist[i].link;

          this.gameinput = '';
          this.filteredlist = [];
          this.imagelist = [];
        }
      }
    },
    searchGame(){
      var searchingname;
      var gameinputlower = this.gameinput.toLowerCase();
      this.filteredlist = [];
      this.imagelist = [];
      for (var i = 0; i < this.gamelist.length+1; i += 1){
        searchingname = this.gamelist[i].name.toLowerCase();
        if((searchingname.includes(gameinputlower))&&(gameinputlower.length>=3)){
          if(this.filteredlist.length < 3){
            this.filteredlist.push(this.gamelist[i].name);
            this.imagelist.push(this.gamelist[i].image)
          }else{
            this.openederrordiv = true;
          }
        }
      }
    },
  },
};
</script>

<style>
.infoandlink{
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.steambtn{
  background-color: transparent;
  border: none;
  margin-right: 30px;
  cursor: pointer;
  transition: 0.2s;
  color: #fff;
}
.steambtn:hover{
  color: rgb(161, 161, 161);
}
.fa-steam{
  font-size: 70px;
}
.maininfos{
  margin-left: 5px;
}
.info{
  margin-top: 5px;
}
.dprr{
  margin-top: 5px;
  margin-left: 3px;
}
.infodiv{
  display: flex;
}
.developer , .publisher{
  color: rgb(255, 255, 113);
}
.reviewcount , .reviews{
  color: rgb(128, 255, 86);
}
.downdiv{
  color: #fff;
  display: flex;
  justify-content: center;
}
.showimg{
  width: 600px;
  height: 300px;
  border-radius: 30px;
}
.gamenamediv{
  margin-top: 30px;
  display: flex;
  justify-content: center;
  align-items: center;
}
.imganddesc{
  margin-top: 20px;
  display: flex;
}
.showdesc{
  font-size: 25px;
  width: 400px;
  margin-left: 5px;
  margin-top: 5px;
}
.pricediv{
  margin-top: 20px;
  display: flex;
  justify-content:center;
  align-items: end;
}
.price{
  font-size: large;
  background-color: greenyellow;
  padding: 12px;
  border-radius: 100px;
  color: #2a2a2a;
  
}
.releasedatediv{
  display: flex;
  justify-content: center;
  align-items: center;
}
*{
  margin: 0;
  padding: 0;
  font-family: Arial, "Helvetica Neue", Helvetica, sans-serif;
}
.main{
  width: 100%;
  height: 100vh;
  background-color: #202226;
}
.updiv{
  width: 100%;
  height: 8vh;
  display: flex;
  justify-content: center;
}
.downdiv{
  width: 100%;
  height: 92vh;
}
.container{
  height: 400px;
}
.inputdiv{
  margin-top: 30px;
}
.input{
  font-size: 30px;
  padding-left: 20px;
  width: 550px;
  height: 40px;
  border-radius: 100px;
  border: 1px solid rgb(119, 119, 119);
  background-color: transparent;
  caret-color : white;
  color: white;
}
.input:focus{
  outline: none;
}
.errordiv{
  height: 50px;
  margin-top: 5px;
  width: 562px;
  margin-left: 1px;
  display: flex;
  justify-content: center;
  align-items: center;
  border-radius: 25px;
  background-color: white;
  padding: 2px;
  position:absolute;
}
.recommendedgamesdiv{
  margin-top: 5px;
  width: 562px;
  margin-left: 1px;
  display: flex;
  border-radius: 25px;
  background-color: white;
  position:absolute;
  padding-left: 2px;
  padding-right: 2px;
}
.imageside{
  width: 35%;
}
.nameside{
  width: 65%;
}
li{
  height: 100px;
  list-style-type: none;
  margin-bottom: 2px;
  margin-top: 2px;
}
.liname{
  justify-content: center;
  display: flex;
  align-items: center;
  color: #212121;
  border-radius: 30px;
  cursor: pointer;
}
.liname:hover{
  background-color: #aaaaaa;
}
.liimage{
  cursor: pointer;
}
.image{
  height: 100px;
  width: 100%;
  border-radius: 30px;
}
.namebtn{
  width: 100%;
  height: 100px;
  background-color: transparent;
  border: none;
  font-size: large;
  cursor: pointer;
}
</style>
