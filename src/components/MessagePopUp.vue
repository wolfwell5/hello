<template>

  <div class="messageBox"
       style="outline: #42b983 solid 1px; border: aqua 1px;width: 400px;height: 400px;    text-align-last: start">
    <div style="float:left;width:40%; ;margin-top:5px;margin-left: 15px;">交易线</div>
    <div style="float:right;width:51%; "><span @click="closePop"
                                               style="margin-left: 180px;margin-top: 5px;">X</span>
    </div>
    <div>
      <hr style="width: inherit"/>
    </div>

    <div style="margin: 0 auto; width: 90%;border: solid 2px;">
      <input @keyup="filterInput" v-model="inputText" type="search" placeholder="search..." style="width: 90%"/>
      <span>🔍</span>
    </div>

    <div style="width: 80%;height: 100px;outline: #42b983 solid 1px;margin: 30px;overflow-y: scroll;">
      <table>
        <tr v-for="(item, index) in dataList" :key="item.id">
          <input @change="checkedBox(item.id)" type="checkbox" :value="item.id"
                 :checked="choose.indexOf(item.id)>=0"/>
          <span> &nbsp;&nbsp;{{item.name}}</span>
        </tr>
      </table>
    </div>

    <div style="width: 80%;height: 100px;outline: #42b983 solid 1px;margin: 30px;;overflow-y: scroll;">
      <table>
        <div v-for="(item, index) in dataList" :key="item.id" v-show="choose.indexOf(item.id)>=0"
             style="border:black 1px dashed; width: 100px;">
          <tr>
            <input type="checkbox" v-model="choose" :value="item.id"/>
            <span> &nbsp;&nbsp;{{item.name}}</span>
            <span @click="checkedBox(item.id)" style="margin-left: 10px"> ×</span>
          </tr>
        </div>
      </table>
    </div>

    <div style="">
      <input type="button" value="清空" @click="clearChecked" style="margin-left: 20px;padding-left: 15px;width: 60px;"/>
      <input type="button" value="取消" @click="closePop" style="margin-left: 150px;width: 60px;padding-left: 15px;"/>
      <input type="button" value="确定" style="margin-left: 10px; width: 60px;padding-left: 15px;"/>

    </div>
  </div>

</template>

<script>
    export default {
        name: "messageBox",
        data() {
            return {
                dataListMock: [
                    {id: 0, name: 'a1', checked: false},
                    {id: 1, name: 'ac1', checked: false},
                    {id: 2, name: 'aa11', checked: false},
                    {id: 3, name: 'b11', checked: false},
                    {id: 4, name: 'bb22', checked: false},
                ],
                dataList: [],
                choose: [],
                inputText: '',
            }
        },
        watch: {
            inputText: function (n, o) {
                this.filterInput();
            },
        },
        props: {
            title: {
                default:
                    ''
            },
            content: {
                default:
                    ''
            },
            cancel: {
                default:
                    'cancel'
            },
            ok: {
                default:
                    'ok'
            },
        },
        mounted() {
            this.dataList = this.dataListMock;
        },
        methods: {
            closePop() {
                this.$emit('close-pop');
                this.choose = [];
            }
            ,
            checkedBox(id) {
                const idx = this.choose.indexOf(id);
                if (idx >= 0) {
                    this.choose.splice(idx, 1);
                } else {
                    this.choose.push(id);

                }
            }
            ,
            clearChecked() {
                this.choose = [];
            }
            ,
            filterInput() {
                this.dataList = this.dataListMock.filter((obj) => {
                    return obj.name.toString().indexOf(this.inputText) >= 0;
                });
            }
            ,
        }
        ,
    }
</script>

<style scoped>
  .messageBox {
    width: 450px;
    height: 500px;
    border: 1px solid #ccc;
    border-radius: 4px;
    background: lightcyan;
    box-shadow: 1px 1px 1px 1px;
    left: 50%;
    top: 50%;
    position: fixed;
    z-index: 1001;
    transform: translate(-50%, -50%);

  }

  .messageBox h2 {
    text-align: center;
    line-height: 40px;
    font-size: 18px;
  }

  .messageBox p {
    text-align: center;
    line-height: 40px;
  }

  .messageBox > div {
    display: flex;
    /*position: absolute;*/
    bottom: 0;
    width: 100%;
  }

  .messageBox > div div {
    flex: 1;
    text-align: center;
    /*line-height: 30px;*/
    border-right: 1px solid #ccc;

  }

  .messageBox > div div:last-child {
    border: none;
  }
</style>
