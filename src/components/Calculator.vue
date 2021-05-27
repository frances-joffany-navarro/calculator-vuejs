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
            operator: '',
            arr: [],
            result: ''
        }
    },
    methods: {
        clear() {
            this.content = '0',
            this.operator = '',
            this.arr = [],
            this.result = ''
        },

        sign() {
            if(this.content !== '0'){
                if(this.operator === ''){
                    if(this.content[0] !== '-' && this.content !== '' ){
                        this.content = '-' + this.content                
                    } else {
                        this.content = this.content.substring(1)
                    }
                } else {
                    if(this.operator === '*'){
                        this.operator = 'x'
                    }else if(this.operator === '/'){
                        this.operator = '÷'
                    }
                    
                    this.arr = this.content.split(this.operator);
                    if(this.arr[1][0] !== '-' && this.arr[1].length > 0 ){        
                        console.log(this.arr[0] + this.operator + '-' + this.arr[1]  )               
                        this.content = this.arr[0] + this.operator + '-' + this.arr[1]             
                    } else {
                        console.log(this.arr[0] + this.operator + this.arr[1].substring(1))
                        this.content = this.arr[0] + this.operator + this.arr[1].substring(1)
                    }
                }                
            }      
            this.arr = []      
        },
        rounded(number){
            return Math.round((number + Number.EPSILON) * 100000000) / 100000000
        },
        percent(){
            if(this.operator === ''){
                this.content = String((parseFloat(this.content) / 100).toExponential(4))
            }            
        },
        getNumber(number){
            if(this.content === '0'){
                this.content = ''
            }
            if(this.content.length < 12){
                this.content += number
            }            
        },
        add(){
            if(this.operator === ''){
                if(this.content[this.content.length-1] !== '.'){                
                    this.operator = '+'
                    this.content += '+'
                }
            }
        },
        minus(){
            if(this.operator === ''){
                if(this.content[this.content.length-1] !== '.'){
                    this.operator = '-'
                    this.content += '-'
                }
            }
        },
        multiply(){
            if(this.operator === ''){
                if(this.content[this.content.length-1] !== '.'){
                    this.operator = '*'
                    this.content += 'x'
                }
            }
        },
        divide(){
            if(this.operator === ''){
                if(this.content[this.content.length-1] !== '.'){
                    this.operator = '/'
                    this.content += '÷'  
                }
            }
        },
        dot(){
            if(this.operator === ''){
                if(this.content.indexOf('.') < 0){
                    this.content = this.content.concat('.')
                }
            } else {
                this.arr = this.content.split(this.operator);
                if(this.arr[1].length > 0){
                    if(this.arr[1].indexOf('.') < 0){
                        this.content = this.content.concat('.')
                    }
                }
            }
            this.arr = []            
        },
        equal(){
            
            if(this.content.indexOf('x') > 0){
                this.operator = 'x'
            } else if (this.content.indexOf('÷') > 0){
                this.operator = '÷'
            }         

            if(this.content[this.content.length-1] !== '.' && this.content[this.content.length-1] !== this.operator){
                switch (this.operator) {
                    case '+':                    
                        console.log(this.content)
                        this.arr = this.content.split('+');
                        this.content = String(this.rounded(parseFloat(this.arr[0]) + parseFloat(this.arr[1])))
                        this.arr = []
                        this.operator = '' 

                        break;

                    case '-':
                        console.log(this.content)
                        this.arr = this.content.split('-');
                        this.content = String(this.rounded(parseFloat(this.arr[0]) - parseFloat(this.arr[1])))
                        
                        this.arr = []
                        this.operator = ''
                        break;

                    case '*' :
                    case 'x' :
                        console.log(this.content)
                        this.arr = this.content.split('x');
                        this.content = String(this.rounded(parseFloat(this.arr[0]) * parseFloat(this.arr[1])))
                        //this.content = String(parseFloat(this.previous) * parseFloat(this.content))
                        this.arr = []
                        this.operator = ''
                        break;
                    
                    case '/' :
                    case '÷' :
                        this.arr = this.content.split('÷');
                        this.content = String(this.rounded(parseFloat(this.arr[0]) / parseFloat(this.arr[1])))
                        
                        this.arr = []
                        this.operator = ''
                        break;
                
                    default:
                        console.log("operator no valid")
                        break;
                }
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