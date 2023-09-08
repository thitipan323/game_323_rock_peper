<script setup>
import { ref,} from 'vue'
/*play1*/
const win_count_player1 = ref(0)
const draw_count_player1 = ref(0)
const loss_count_player1 = ref(0)
/*play2*/
const win_count_player2 = ref(0)
const draw_count_player2 = ref(0)
const loss_count_player2 = ref(0)


const player1_choose = ref('');
const player2_choose = ref('');
const result = ref('');

const control_game = {
	'rock': {
		'rock': 'เสมอ',
		'peper': 'แพ้',
		'Scissors': 'ชนะ',
    'love': 'แพ้'
	},

  'Scissors': {
		'rock': 'แพ้',
		'peper': 'ชนะ',
		'Scissors': 'เสมอ',
    'love': 'แพ้'
	},

	'peper': {
		'rock': 'ชนะ',
		'peper': 'เสมอ',
		'Scissors': 'แพ้',
    'love': 'แพ้'
	},
	
  'love': {
		'rock': 'ชนะ',
		'peper': 'ชนะ',
		'Scissors': 'ชนะ',
    'love': 'เสมอ'
	}

}


const choiceImages = {
  'rock': 'https://cdn.discordapp.com/attachments/1004965415870546035/1149379780215591082/scissors.png',
  'peper': 'https://cdn.discordapp.com/attachments/1004965415870546035/1149580619643367545/PinClipart.com_rock-paper-scissors-clip_5360310.png',
  'Scissors': 'https://cdn.discordapp.com/attachments/1004965415870546035/1149579032145436712/111-1114370_rock-paper-scissors-rock-paper-scissors-clipart.png',
  'love': 'https://i.kym-cdn.com/photos/images/original/000/934/145/deb.gif',
};



function getRandomChoice() {
  const choices = ['rock', 'peper', 'Scissors','love'];
  return choices[Math.floor(Math.random() * choices.length)];
}

function display_answer() {
  player1_choose.value = getRandomChoice();
  player2_choose.value = getRandomChoice();

  const out_result = control_game[player1_choose.value][player2_choose.value];

  if (out_result === 'ชนะ') {
    win_count_player1.value++;
    loss_count_player2.value++;
    result.value = 'Player 1 ชนะ';
  } else if (out_result === 'แพ้') {
    win_count_player2.value++;
    loss_count_player1.value++;
    result.value = 'Player 2 ชนะ';
  } else {
    draw_count_player1.value++;
    draw_count_player2.value++;
    result.value = 'เสมอ';
  }
}

function reset_round() {
  player1_choose.value = '';
  player2_choose.value = '';
  result.value = '';
  win_count_player1.value = 0;
  draw_count_player1.value = 0;
  loss_count_player1.value = 0;
  win_count_player2.value = 0;
  draw_count_player2.value = 0;
  loss_count_player2.value = 0;
}



</script>

<template>
  <div class="con_all">
    <div class="box_title">
			<div class="text_title">เกมเป่ายิ๊งฉุบ</div>
      </div>

      <div class="con_game">
        <div class="box_1" id="box_play1">
          Player 1 : ออก {{ player1_choose }}
          <img v-if="!player1_choose" src="https://cdn.discordapp.com/attachments/1004965415870546035/1149593613643288586/kisspng-clip-art-vector-graphics-openclipart-image-what-are-you-binge-watching-playbuzz-5b6824b2056438.8772807715335517940221.png" alt="Player 1 Default" class="box_img" />
          <img v-else :src="choiceImages[player1_choose]" alt="Player 1 Choice" class="box_img" />
        </div>
        <div class="box_2" id="box_play2">
          Player 2 : ออก {{ player2_choose }}
          <img v-if="!player2_choose" src="https://cdn.discordapp.com/attachments/1004965415870546035/1149593613643288586/kisspng-clip-art-vector-graphics-openclipart-image-what-are-you-binge-watching-playbuzz-5b6824b2056438.8772807715335517940221.png" alt="Player 2 Default" class="box_img" />
          <img v-else :src="choiceImages[player2_choose]" alt="Player 2 Choice" class="box_img" />
        </div>
      </div>

    <div class="start_buttom">
      <button @click="display_answer" class="buttom_start"> เป่ายิ๊งฉุบบบบบ </button>
    </div>

  <div class="con_all_score"> 
    <div class="contrainer_score">
      <div class="box_score1"> แต้ม Player1 <br> {{ win_count_player1 }}  </div>  
      </div>
    <div class="contrainer_score">
      <div class="box_score2"> แต้ม Player2 <br> {{ win_count_player2 }}  </div>  
      </div>
  </div> 
    <div class="newgame">
      <button @click="reset_round" class="buttom_new"> เริ่มใหม่ </button>
    </div>

  </div>    

  

</template>

<style>



/*ALl body*/
:root {
  text-align: center;
  font-family: 'Itim', cursive;
  font-size: 24px;
  line-height: 1.5;
  font-weight: 400;
  color-scheme: light dark;
  color: #ffffff;
  background-color: #ffffff;
  font-synthesis: none;
  text-rendering: optimizeLegibility;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  -webkit-text-size-adjust: 100%;

}

#app {
  
  margin:  auto;
  padding: 6rem;
  text-align: center;
  background-color: #fff;
}

*{
  padding: 10px;
}


/*background*/
.con_all{
  border-radius: 50px;
  padding-left:1rem;
  background-image: url('https://images.pexels.com/photos/163077/mario-yoschi-figures-funny-163077.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1');
  
}

.box_play1 .box_1{
  padding-left: 2rem;
  max-width: 100px;
  
}


.con_game{
  display: grid;
  grid-template-columns: 1fr 1fr;
  margin-left: 300px;
  margin-right: 250px;
  padding: 50px;
  justify-content: center;
}

.box_img {
  width: 150px;
  height: 150px; 
}


.contrainer_score2{
  display: grid;
  grid-template-columns: 1fr 1fr 
  
}

.con_all_score{
  border:2px solid rgb(186, 157, 136);
  border-radius: 50px;
  margin-left: 50px;
  margin-right: 50px;
  font-size: 25px;
}


.text_title{
  background-color: #2b4a4a;
  width: 500px;
  height: 70px;
  border-radius: 50px;
  margin: auto; 
  display: flex;
  align-items: center;
  justify-content: center;  
  font-size: 32px;

}


.buttom_new{
  padding: 20px;
  width: 7rem;
  height: 2.5rem;
  background-color: red;
  border-radius: 8px;
  border: 1px solid transparent;
  font-size: 1em;
  font-weight: 500;
  font-family: inherit;
  color: #242424;
  cursor: pointer;
  transition: border-color 0.25s;
}

.buttom_start:hover{
  box-shadow: 0 3px 6px rgb(0, 0, 0.16),
  0 3px 6px rgb(0, 0, 0.23);
  transform:translate(0px, -8px) ;
  transition: 0.4s;
  padding: 15px;
  border: 2px solid var(--text--color);
  background-image: linear-gradient( 135deg, #F05F57 10%, #360940 100%);
  color: rgb(135, 135, 135);
}


.buttom_start{
  padding: 20px;
  width: 9rem;
  height: 2.5rem;
  background-image: linear-gradient( 135deg, #81FBB8 10%, #28C76F 100%);
  border-radius: 8px;
  border: 1px solid transparent;
  font-size: 1em;
  font-weight: 500;
  font-family: inherit;
  color: #242424;
  cursor: pointer;
  transition: border-color 0.25s;
}




.newgame  {
  color: #954a4a; /* สีข้อความของปุ่ม */
  padding: 10px 20px; /* ขนาดของปุ่ม */
  border: none; /* ลบเส้นขอบของปุ่ม */
  border-radius: 5px; /* ทำให้มีมุมโค้งบนปุ่ม */
  cursor: pointer; /* เปลี่ยนรูปตัวชี้เป็นมือเมื่อชี้ที่ปุ่ม */
  margin-top: 20px;
}

.button_new:hover {
  box-shadow: 0 3px 6px rgb(0, 0, 0.16),
  
}

@import url('https://fonts.googleapis.com/css2?family=Itim&display=swap');
</style>