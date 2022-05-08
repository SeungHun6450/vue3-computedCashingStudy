<template>
  <!-- 이중 중괄호 문법 사이에 표현식을 작성할 수 있다. -->
  <h1>{{ msg + '??' }}</h1>
  <h1>{{ msg.split('').reverse().join('') }}</h1>
  <!-- 여러 번 반복 시 메소드 대신 computed의 캐시 기능을 사용한다. -->
  <button @click="add">
    ADD
  </button>
  <h1>{{ reversedMessage }}</h1>
  <h1>{{ reversedMessage }}</h1>
  <h1>{{ reversedMessage }}</h1>
  <h1>{{ reversedMessage }}</h1>
</template>

<script>
  export default {
    data() {
      return {
        // Getter, Setter: 값을 얻어내거나 값을 지정하는 용도로 사용할 수 있다.
        msg: 'Hello Computed!'
      }
    },
    // 계산된 데이터: 캐싱기능이 존재 한 번 연산해둔 값이 있다면 재 연산 하지 않는다.
    // 아래의 reverseMessage() 메소드 처럼 나올 때 마다 연산해서 출력하지 않아 부담이 줄어 든다.
    // 즉, 데이터를 최적화 하는 용도로 사용할 수 있다.
    // 원본의 데이터를 손상시키지 않고 계산을 한다.
    computed: {
      // Getter
      // reversedMessage() {
      //   return this.msg.split('').reverse().join('')
      // }
      // Getter, Setter
      reversedMessage: {
        // 값을 얻어내는 용도
        get() {
          return this.msg.split('').reverse().join('')
        },
        // 값을 할당하는 용도
        set(v) { 
          // 1. 버튼을 누를 경우 아래의 add()가 실행된다.
          // 2. reversedMessage에 '!?'가 + 되면서 v에 들어온다.
          // 3. v가 msg 데이터에 할당이 된다.
          // 4. 변경된 값이 get()으로 가서 새로 변경된 값을 return통해 반환하여 화면에 출력
          this.msg = v
        }
      }
    },
    methods: {
      reverseMessage() {
        return this.msg.split('').reverse().join('')
      },
      add() {
        // Getter인 경우 읽기 전용(Readonly)이기 때문에 할당 연산자를 통해 값을 할당하더라도 반응적으로 동작을 할 수 없다.
        this.reversedMessage += '!?'
      }
    }
  }
</script>