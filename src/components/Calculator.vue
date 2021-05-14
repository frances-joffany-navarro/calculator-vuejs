<template>
    <div>
        <header>
            <h1>Calculator using VueJS</h1>
        </header>
        <div class="grid-container">
            <div class="display">{{ content }}</div>
            <div class="item sign" @click="clear">C</div>
            <div class="item sign" @click="sign">+/-</div>
            <div class="item sign" @click="percent">%</div>        
            <div class="item sign" @click="divide">÷</div>
            <div class="item" @click="getNumber('7')">7</div>
            <div class="item" @click="getNumber('8')">8</div>
            <div class="item" @click="getNumber('9')">9</div>
            <div class="item sign" @click="multiply">x</div>
            <div class="item" @click="getNumber('4')">4</div>
            <div class="item" @click="getNumber('5')">5</div>
            <div class="item" @click="getNumber('6')">6</div>
            <div class="item sign" @click="minus">-</div>
            <div class="item" @click="getNumber('1')">1</div>
            <div class="item" @click="getNumber('2')">2</div>
            <div class="item" @click="getNumber('3')">3</div>
            <div class="item sign" @click="add">+</div>
            <div class="item zero" @click="getNumber('0')">0</div>
            <div class="item" @click="dot">.</div>
            <div class="item equal" @click="equal">=</div>
        </div>

    </div>
</template>

<script>
export default {
    data() {
        return {
            content: '0',
            previous: 0,
            operator: ''
        }
    },
    methods: {
        clear() {
            this.content = '0'
        },
        sign() {
            if(this.content !== '0'){
                if(this.content[0]!== '-' && this.content !== ''){
                this.content = '-' + this.content                
                } else {
                    this.content = this.content.substring(1)
                }
            }            
        },
        percent(){
            this.content = String(parseFloat(this.content) / 100)
        },
        getNumber(number){
            if(this.content === '0'){
                this.content = ''
            }
            this.content += number
        },
        getPrevious(){
            this.previous = this.content
            this.content = '0'
        },
        divide(){
            this.getPrevious()
            this.operator = '/' 
        },
        multiply(){
            this.getPrevious()
            this.operator = '*'
        },
        minus(){
            this.getPrevious()
            this.operator = '-'
        },
        add(){
            this.getPrevious()
            this.operator = '+'
        },
        dot(){
            if(this.content.indexOf('.') < 0){
                this.content = this.content.concat('.')
            }
        },
        equal(){
            switch (this.operator) {
                case '+':                    
                    this.content = String(parseFloat(this.previous) + parseFloat(this.content))
                    this.operator = ''
                    break;

                case '-':
                    
                    this.content = String(parseFloat(this.previous) - parseFloat(this.content))
                    this.operator = ''
                    break;

                case '*':
                    this.content = String(parseFloat(this.previous) * parseFloat(this.content))
                    this.operator = ''
                    break;
                
                case '/':
                    this.content = String(parseFloat(this.previous) / parseFloat(this.content))
                    this.operator = ''
                    break;
            
                default:
                    break;
            }
        }

    },
}
</script>

<style>
.grid-container {
    display: grid;
    grid-template-columns: auto auto auto auto;
    grid-template-rows: 70px 50px 50px 50px 50px 50px;
    background: rgb(211, 211, 211);
    font-size: 20px;
    color: black;
    width: 320px;
    margin: 0 auto;
    grid-gap: 3px;
    padding: 3px;
}
.display {
    grid-column: 1/5;
    padding: 20px;
    text-align: end;
    font-size: 40px;
    border: 1px solid rgba(255, 255, 255, 0.8);
}

.zero {grid-column: 1/3;}

.item {
    padding: 15px;
    border: 1px solid rgba(255, 255, 255, 0.8);
}
.equal {background-color: orange;}

.sign {background-color: rgb(182, 181, 181);}
</style>