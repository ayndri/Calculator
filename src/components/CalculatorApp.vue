<template>
    <div class="wrap-head">
        <div class="display">
            <span>{{ Number(current).toLocaleString() || '0' }}</span>
        </div>
        <div class="calculator">

            <div @click="clear" class="btn top">AC</div>
            <div @click="sign" class="btn top">+/-</div>
            <div @click="percent" class="btn top">%</div>
            <div @click="divide" class="btn operator" :class="{ 'active': index == 'divide' }">÷</div>
            <div @click="append('7')" class="btn number">7</div>
            <div @click="append('8')" class="btn number">8</div>
            <div @click="append('9')" class="btn number">9</div>
            <div @click="times" class="btn operator" :class="{ 'active': index == 'times' }">x</div>
            <div @click="append('4')" class="btn number">4</div>
            <div @click="append('5')" class="btn number">5</div>
            <div @click="append('6')" class="btn number">6</div>
            <div @click="minus" class="btn operator" :class="{ 'active': index == 'minus' }">-</div>
            <div @click="append('1')" class="btn number">1</div>
            <div @click="append('2')" class="btn number">2</div>
            <div @click="append('3')" class="btn number">3</div>
            <div @click="add" class="btn operator" :class="{ 'active': index == 'add' }">+</div>
            <div @click="clearOne" class="btn number">C</div>
            <div @click="append('0')" class="btn number zero">0</div>
            <div @click="dot" class="btn number">.</div>
            <div @click="equal" class="btn operator">=</div>
        </div>
    </div>
</template>
  
<script>
export default {
    data() {
        return {
            previous: null,
            current: '',
            operator: null,
            operatorClicked: false,
            index: '',
            darkMode: false
        }
    },
    methods: {
        clear() {
            this.current = '';
            this.index = "";
        },
        sign() {
            this.current = this.current.charAt(0) === '-' ?
                this.current.slice(1) : `-${this.current}`;
            this.index = "";
        },
        percent() {
            this.current = `${parseFloat(this.current) / 100}`
            this.index = "";
        },
        append(number) {

            if (this.current.length < 9) {
                if (this.operatorClicked) {
                    this.current = '';
                    this.operatorClicked = false;
                }

                this.current = `${this.current}${number}`
                this.index = "";
            }


        },
        dot() {
            if (this.current.indexOf('.') === -1) {
                this.append('.');
            }
            this.index = "";
        },
        setPrevious() {

            if (this.previous != null) {
                this.current = `${this.operator(
                    parseFloat(this.current),
                    parseFloat(this.previous)
                )}`;
            }

            this.previous = this.current;

        },
        divide() {
            this.setPrevious();
            this.operator = (a, b) => b / a;
            this.operatorClicked = true;
            this.index = "divide";
        },
        times() {
            this.setPrevious();
            this.operator = (a, b) => a * b;
            this.operatorClicked = true;
            this.index = "times";
        },
        minus() {
            this.setPrevious();
            this.operator = (a, b) => b - a;
            this.operatorClicked = true;
            this.index = "minus";
        },
        add() {
            this.setPrevious();
            this.operator = (a, b) => a + b;
            this.operatorClicked = true;
            this.index = "add";
        },
        equal() {
            this.current = `${this.operator(
                parseFloat(this.current),
                parseFloat(this.previous)
            )}`;
            this.previous = null;
            this.index = "";
        },
        clearOne() {
            this.current = this.current.slice(0, this.current.length - 1);
            if (this.current.length === 0) {
                this.current = '';
            }
            this.index = "";
        }
    },
    mounted() {
        // Support keyboard entry
        window.addEventListener('keyup', event => {
            if (event.key.match(/^[0-9]*$/)) return this.append(event.key);
            if (event.key === '*') return this.times();
            if (event.key === '+') return this.add();
            if (event.key === '-') return this.minus();
            if (event.key === '/') return this.divide();
            if (event.key === 'Delete') return this.clear();
            if (event.key === 'Backspace') return this.clearOne();
            if (event.key === 'Enter') return this.equal();
            if (event.key === '.' || event.key === ',') return this.dot();
        });
    }
}
</script>
  
  <!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.wrap-head {
    margin: 0 auto;
    width: 400px;
    border-radius: 20px;
    background-color: #23252c;
}

.calculator {
    font-size: 24px;
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    grid-auto-rows: minmax(50px, auto);
    background-color: #2a2d35;
    padding: 20px;
    border-radius: 30px;
}

.display {
    grid-column: 1 / 5;
    background-color: #23252c;
    color: #f2f2f2;
    height: 300px;
    display: flex;
    align-items: flex-end;
    justify-content: flex-end;
    padding: 30px;
    font-size: 50px;
    border-radius: 30px 30px 0px 0px;
}

/* .zero {
        grid-column: 1/2;
    } */

.active {
    background-color: #d76c68 !important;
    color: #282b32 !important;
}

.btn {
    background-color: #282b32;
    display: flex;
    align-items: center;
    justify-content: center;
    margin: 10px 10px;
    padding: 15px;
    border-radius: 10px;
}

.number {
    color: #fff;
}

.top {
    color: #78fad8;
}

.operator {
    color: #d76c68;
}

</style>
  