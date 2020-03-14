<template>
  <div>
    <div class="qui-list">
      <input type="button" class="list-tips" style="color: #42b983;font-size: 20px;outline: #2c3e50 1px dashed"
             :value="tipsText"/>
      <qui-btn @btnClickEvent="btnClickEvent" :msg=msg class="small"></qui-btn>
    </div>


    <message-box
      style=""
      @close-pop="fClosePop"
      v-show="showMsg"
      title="11"
      content="22"
    />


  </div>
</template>

<script>
    import quiButton from '../components/quiButton.vue'
    import MessageBox from "./MessagePopUp";


    export default {

        props: {
            msg: {
                default: '下载'
            },
            tipsText: {
                default: '默认的文案'
            }
        },
        components: {
            MessageBox,
            'qui-btn': quiButton,
        },
        methods: {
            btnClickEvent: function (msg) {
                // console.log(msg)
                this.showPop = !this.showPop;
                this.showMsg = !this.showMsg;
                // alert('按钮点击事件')
            },
            fClosePop() {
                this.showMsg = false;
            },
        },
        data() {
            return {
                showPop: false,
                showMsg: false,
            }
        },
    }

</script>
