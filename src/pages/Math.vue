<template>
  <q-page class="">
    <q-parallax
      :height="200"
      :speed="1"
    >
    <template v-slot:media>
        <img src="https://png.pngtree.com/background/20210712/original/pngtree-cute-hand-drawn-style-mathematics-education-pink-plaid-background-picture-image_1176715.jpg">
      </template>
      <div class="absolute-full text-subtitle2 flex flex-center">
        <h4>📚 Gaussian elimination calculation step-by-step 📝</h4>
      </div>
    </q-parallax>
    <!-- <div class="text-h4 q-pa-md">
      Gaussian elimination calculation step-by-step
    </div> -->
    <!-- <div class="text-white"></div> -->
    <!-- <div class="text-white">OKPKPKPKPPPKPKPKPKPKPKPKPKPKPKPKPKPKPKPKPKPKPKPKPKPKPKPKPKPKPKPKPKPKPKPKPKPKPKPKPKOKOKOOKOKOOOKOKOKOKOOKOKOKOKOKOKKOKOKOKOKOKOKOKOKOKOKOKOKOKOKOKOKOKOKOKOKOKOKOKOKOKOKOKOKOKOKOKOKOKOKOKOKOKOKOKOKOKKOKOOKKOKOKOKOKOKOKOKOOKOKKOKOKOKOKOKOKKOKOKOKOKOKOKOKOKOKOKOKOKO</div> -->

    <div class="q-pt-xl q-px-xl padding">
        <div class="text-h6">
          Size of the matrix:
        </div>
        <div class="row">
          <div class="col-2 q-pb-md" type="number">
            <q-input dense v-model="ii" label="system size: i"/>
          </div>
          <div class="col-0 text-h6 flex flex-center q-px-md"> × </div>
          <div class="col-2">
            <q-input dense v-model="jj" label="system size: j" type="number"/>
          </div>
          <div class="col-2 q-pl-sm">
            <q-btn color="primary" icon="done_outline" label="Set system" @click="sendMatrix()"/>
          </div>
        </div>
    </div>


    <div class="column">
      <div class="row q-py-md q-px-xl">
        <div class="col-1 q-px-md" v-for="matrixj in intNumber(j - 1)" :key="matrixj"> X{{ matrixj }}</div>
        <div class="col-0 text-h6 flex flex-center q-px-md" v-if="sent"> = </div>
        <div class="col-1 q-px-md" v-if="sent"> b </div>
      </div>

      <div class="row q-py-md q-px-xl" v-for="matrixi in intNumber(i)" :key="matrixi">
        <div class="col-1 q-px-md" v-for="matrixj in intNumber(j - 1)" :key="matrixj">
          <q-input v-model="a[matrixi - 1][matrixj - 1]" dense :label="label(matrixi, matrixj)" stack-label/>
        </div>
        <div class="col-0 text-h6 flex flex-center q-px-md"> = </div>
        <div class="col q-px-md">
          <q-input v-model="a[matrixi - 1][j - 1]" dense :label="label(matrixi, j)" stack-label/>
        </div>
      </div>
    </div>

    <div class="q-px-xl row">
      <!-- <q-card class="q-pa-md"> -->
        <div>

        </div>
        <div class="col-2 q-pb-md q-pr-xl">
          <q-btn color="primary" icon="clear" label="Clear" @click="clearAll()"/>
        </div>
        <div class="col-2 q-pl-md">
        <q-btn color="primary" icon="drive_file_rename_outline"
        label="Answer" @click="submitAnswer"/>
        </div>
      <!-- </q-card> -->
    </div>

    <div class="q-pt-md q-px-xl" v-for="re in result.length" :key="re">
      {{ result[re] }}
    </div>

  </q-page>
</template>

<script>
import { defineComponent } from 'vue'



export default defineComponent({
  name: 'IndexPage',
  data(){
    return{
      ii: null,
      jj: null,
      i: null,
      j: null,
      a:[[11, 12, 13, 14],[21, 22, 23, 24]],
      b:[[11, 12, 13, 14],[21, 22, 23, 24]],
      empty: [],
      k: 0,
      p: 0,

      sent: false,

      check: 0,
      checki: 0,
      checkj: 0,
      order: 0,
      result: [],
    }
  },
  methods:{
    intNumber(num){
      let i = 0
      if (num > 0)
        for (i = 0; i < num; i++){
      }
      // console.log(i)
      return i;
    },
    roundNumber(num){
      return Math.round(num * 100) / 100;
    },
    sendMatrix(){
      this.i = this.intNumber(this.ii);
      this.j = this.intNumber(this.jj);

      if (this.i == null || this.j == null) {
        this.i = null;
        this.j = null;
        return;
      }
      if (this.i == 0 || this.j == 0) {
        this.i = null;
        this.j = null;
        return;
      }
      this.sent = true;
      // console.log("i : " + this.i);
      // console.log("j : " + this.j);
      for (this.k = 0; this.k <= this.a.length; this.k++) {
        this.a.pop();
        this.b.pop();
      }
      // console.log(this.a)
      for (this.k = 0; this.k < this.i; this.k++) {
        this.a.push([])
        this.b.push([])
      }

      for (this.k = 0; this.k < this.i; this.k++) {
        for (this.p = 0; this.p < this.j; this.p++) {
          this.a[this.k].push(this.p + this.k)
          this.b[this.k].push(null)
        }
      }

      // for (this.k = 0; this.k < this.i; this.k++) {
      //   for (this.p = 0; this.p < this.j; this.p++) {
      //     this.b = this.intNumber
      //     this.a[this.k].push(this.p + this.k)
      //   }
      // }
      // for (this.k = 0; this.k < this.i; this.k++) {
      //   for (this.p = 0; this.p < this.j; this.p++) {
      //     this.a[this.k][this.p] = this.p + this.k;
      //     console.log(this.a);
      //   }
      // }
      this.clearAll();
    },
    clearAll() {
      for (this.k = 0; this.k < this.i; this.k++) {
        for (this.p = 0; this.p < this.j; this.p++) {
          this.a[this.k][this.p] = null
        }
      }
    },
    submitAnswer() {
      this.checkEmpty();
      for (this.k = 0; this.k < this.i; this.k++) {
        for (this.p = 0; this.p < this.j; this.p++) {
          this.b[this.k][this.p] = this.roundNumber(this.a[this.k][this.p]);
        }
      }

      this.result = [];
      this.result.push("");
      let foundOne = false;
      let outOfOrder = false;
      let allZero = false;
      // let minus = false;
      let x = 0;

      let min = 0;
      // let resultString = "";

      this.checki = 0;
      this.checkj = 0;

      for (let yy = 0; yy < this.j - 1; yy++) {

        // find 1.
        for (x = this.checki; x < this.i; x++) {
          // console.log(x + " " + this.a[x][this.checkj]);
          if (this.a[x][this.checkj] == 1 && foundOne == false) {
            // console.log("Yay");
            foundOne = true;
            if (x != this.checki) {
              outOfOrder = true;
            }
            this.checki++;
            this.checkj++;
            break;
          }
        }

        //didn't find 1 so we make the first one as 1.
        // console.log(this.a[this.checki][this.checkj]);
        if (!foundOne && this.a[this.checki][this.checkj] != 0){
          let divide = this.a[this.checki][this.checkj];
          for (let y = 0; y < this.j; y++) {
            this.a[this.checki][y] /= divide;
          }
          this.checki++;
          this.checkj++;
          foundOne = true;

          this.result.push(" -------- ");
          this.result.push("1/" + this.roundNumber(divide) + " * row" + this.checki + " → row" + this.checki + " : ");
          this.currentA();
          // console.log("divide");
          // console.log(this.result);
        }

        // for (let r = 0; r < this.i; r++) {

        // }

        //didn't find anything.
        // if (!foundOne) {
        //   this.checkj++;
        //   foundOne = true;
        // }

        if (outOfOrder) {
          let temp1 = this.a[this.checki - 1];
          let temp2 = this.a[x];
          this.a[this.checki - 1] = temp2;
          this.a[x] = temp1;
          outOfOrder = false;
          this.result.push(" -------- ");
          this.result.push("swap row" + (this.checki - 1) + " ↔ row" + x + " : ");
          this.currentA();
          // console.log("swap");
          // console.log(this.result);
        }

        if (foundOne) for (let xx = this.checki; xx < this.i; xx++) {
          // if ((this.checkj) == xx) {
          //   this.result.push("- row" + (this.checki) + " * " + this.a[xx][this.checkj - 1] + " + row" + (xx+1) + " → " + "row" +(xx+1) + " :");
          //   this.currentA();
          //   console.log("minus");
          //   console.log(this.result);
          //   }
          let multiply = this.a[xx][this.checkj - 1];
          for (let yyy = 0; yyy < this.j; yyy++) {
            this.a[xx][yyy] -= this.a[this.checki - 1][yyy] * multiply;
            // console.log(this.a[xx][yyy]);
          }
          this.result.push(" -------- ");
          this.result.push("- " + this.roundNumber(multiply) + " * row" + (this.checki) + " + row" + (xx+1) + " → " + "row" +(xx+1) + " : ");
          this.currentA();
          // console.log("minus");
          // console.log(this.result);
        }

        if (!foundOne) {
          this.checkj++;
        }

        foundOne = false;
        // console.log(this.checki);
        // console.log(this.checkj);
      }

      this.result.push(" -------- ");
      this.result.push(" Result ");
      this.result.push(" -------- ");
      let answer = []
      // console.log(this.a)
      // for (this.k = 0; this.k < this.i; this.k++) {
      //   answer.push([]);
      // }

      // for (this.k = 0; this.k < this.i; this.k++) {
      //   for (this.p = 0; this.p < this.j; this.p++) {
      //     answer[this.k].push(0)
      //   }
      // }

      let numAns = 0;
      let noAns = false;
      let noAns2 = false;
      let string = "";
      let string2 = "";

      let xx = 0;
      let yy = 0;

      let zeroGone = true;
      let oneGone = true;
      for (yy = 1; yy <= this.j - 1; yy++) {
        if (this.a[this.i-1][yy-1] != 0) zeroGone = false;
      }
      if (this.a[this.i-1][this.j-1] == 0) oneGone = false;
      if (zeroGone && oneGone) {
        this.result.push("This is system not solvable.");
        return;
      }

      for (xx = this.i; xx > 0; xx--) {
        for (yy = this.j; yy > 0; yy--){
          if (this.a[xx-1][yy-1] == 1) {
            // answer[xx-1][yy-1] = this.a[xx-1][yy-1]
            numAns++;
            break;
          }
        }
      }

      let foundAns = false;
      let ans = 0;

      if (numAns == this.i) {
        for (xx = this.i; xx > 0; xx--) {
          // console.log(this.a[xx-1][this.j-1]);
          for (yy = 1; yy < this.j; yy++) {
            if (this.a[xx-1][yy-1] == 1) {
              this.result.push("X" + (xx) + " = " + this.roundNumber(this.a[xx-1][this.j-1]));
              answer[yy-1] = this.a[xx-1][this.j-1];
              foundAns = true;
              // console.log("HEYEYEYE  " + answer[0][0]);
              break;
            }
          }
          if (foundAns) break;
        }

        let foundagain = false;
        for (xx = this.i - 1; xx > 0; xx--) {
          string = "";
          string2 = "";
          ans = this.a[xx-1][this.j-1];
          foundagain = false;
          // console.log(ans);
          // this.result.push("X" + xx + " :");
          this.result.push(" -------- ");
          for (yy = 1; yy < this.j; yy++){
            if (this.a[xx-1][yy-1] != 0) {
              string += this.roundNumber(this.a[xx-1][yy-1]) + " * X" + yy + " + ";
            }
            if (this.a[xx-1][yy-1] == 1 && !foundagain) {
              string2 += "X" + yy + " = ";
              foundagain = true;
              // answer[]
            }
          }
          for (yy = 1; yy < this.j; yy++){
            if (this.a[xx-1][yy-1] != 0 && answer[yy-1] != null) {
              ans = ans - (this.a[xx-1][yy-1] * answer[yy-1]);
            }
          }
          for (yy = 1; yy < this.j; yy++){
            if (this.a[xx-1][yy-1] == 1) {
              answer[yy-1] = ans;
              break;
            }
          }
          string2 += this.roundNumber(ans) + "";
          string = string.slice(0, string.length - 3);
          string += " = " + this.roundNumber(this.a[xx-1][this.j-1]);
          this.result.push(string);
          this.result.push(string2);
        }
      }

      let foundOneTwo = false;
      if (numAns != this.i) {
        // console.log("HIHIHIHIHI");
        for (xx = this.i; xx > 0; xx--) {
          string = "";
          string2 = "";
          this.result.push(" -------- ");
          foundOneTwo = false;

          for (yy = 1; yy < this.j; yy++){
            if (this.a[xx-1][yy-1] == 1 && !foundOneTwo) {
              // string += "X" + yy + " = ";
              string2 += "X" + yy + " = " + this.a[xx-1][this.j-1];
              foundOneTwo = true;
              continue;
              // break;
            }
            if (foundOneTwo) {
              string2 += " - " + this.roundNumber(this.a[xx-1][yy-1]) +  " * X " + yy
            }
          }
          if (foundOneTwo) {
            for (yy = 1; yy < this.j; yy++){
              if (this.a[xx-1][yy-1] != 0) {
                string += this.roundNumber(this.a[xx-1][yy-1]) + " * X" + yy + " + ";
              }
            }
            string = string.slice(0, string.length - 3);
            string += " = " + this.roundNumber(this.a[xx-1][this.j-1]);
            this.result.push(string);
            this.result.push(string2);
          }


        }
      }

      for (this.k = 0; this.k < this.i; this.k++) {
        for (this.p = 0; this.p < this.j; this.p++) {
          this.a[this.k][this.p] = this.roundNumber(this.b[this.k][this.p]);
        }
      }
    },
    currentA(){
      let s;
      // let ss = ""
      for(let x = 0; x < this.i; x++){
        s = ""
        // ss = ""
        for(let y = 0; y < this.j; y++){
          if (y == this.j - 1) s += " = " + this.roundNumber(this.a[x][y]) + " ";
          else if (y == this.j - 2) s += " " + this.roundNumber(this.a[x][y]) + " [X" + (y+1)+ "]";
          else s += " " + this.roundNumber(this.a[x][y]) + " [X" + (y+1)+ "] + ";
        }
        this.result.push(s);
      }
    },
    checkEmpty(){
      for(let x = 0; x < this.i; x++){
        for(let y = 0; y < this.j; y++){
          if (this.a[x][y] == null) this.a[x][y] = 0;
        }
      }
      // console.log(this.a);
    },
    label(i, j) {
      return i + ", " + j;
    }
  }
})
</script>
