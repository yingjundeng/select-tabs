<style lang="less" scoped>
.page {
  width: 375px;
  margin: 0 auto;
  font-family: PingFang SC;
  font-weight: 500;
  color: rgba(2, 11, 35, 1);
  background-color: #F7F4F8;

  .page-upload {
    width: 100%;
    margin-top: 10px;
    background-color: #fff;
    padding: 15px;

    .text {
      margin-bottom: 10px;
    }
  }

  .save-btn {
    width: 100%;
    padding: 25px 15px;
  }

  .popup-content {
    .cont-title {
      margin: 25px 0 20px 17px;
    }

    .cont-name {
      display: flex;
      flex-direction: row;
      justify-content: flex-start;
      margin: 0 15px;

      .active {
        color: #fff;
        background-image: linear-gradient(#FE6A5F, #FD6063, #F95463, #FB4B6B);
      }

      .contList {
        text-align: center;
        font-size: 13px;
        line-height: 53px;
        width: calc((100% - 24px)/3);
        height: 53px;
        border: 1px solid rgba(221, 221, 221, 1);
        border-radius: 3px;
        margin-right: 12px;

        &:nth-child(3) {
          margin-right: 0px
        }
      }
    }

    .desc-awkn {
      margin: 23px 15px;
      text-align: center;
      font-size: 20px;

      .desc-toAdd {
        height: 10px;
        font-size: 10px;
        color: rgba(164, 169, 173, 1);
        line-height: 15px;
      }

      .select-tabs {
        display: flex;
        flex-direction: row;
        justify-content: flex-start;
        flex-wrap: wrap;
        text-align: center;

        .tabs-list {
          width: calc((100% - 24px)/3);
          height: 39px;
          position: relative;
          color: #fff;
          font-size: 11px;
          line-height: 39px;
          background-image: linear-gradient(#FE6A5F, #FD6063, #F95463, #FB4B6B);
          border-radius: 3px;
          margin: 0 12px 12px 0;

          &:nth-child(3n) {
            margin-right: 0px;
          }

          .close-i {
            position: absolute;
            top: -12px;
            right: 0;
            font-size: 14px;
            width: 14px;
            height: 14px;
            border-radius: 50%;
          }
        }
      }
    }

    .btm-desc {
      display: flex;
      flex-direction: row;
      justify-content: flex-start;
      flex-wrap: wrap;
      text-align: center;
      padding: 0px 15px;

      div {
        width: calc((100% - 12px)/2);
        height: 39px;
        border: 1px solid rgba(221, 221, 221, 1);
        border-radius: 3px;
        line-height: 39px;
        margin: 0px 6px 12px 0;

        &:nth-child(2n) {
          margin-right: 0px;
        }

      }

      .isSelsect {
        box-shadow: inset 0px 0px 3px 1px rgb(102, 101, 101);
        ;
      }
    }

  }
}
</style>
<style lang="less">

</style>

<template>
<div class="page">
  <div class="popup-content">
    <div class="cont-title">问题类型</div>
    <div class="cont-name">
      <div v-for="(item,index) in tabList" :class="{active:active===index,contList:'contList'}" @click="handleActive(item,index)" :key="index">
        {{item.name}}
      </div>
    </div>

    <div class="cont-title">详细问题</div>
    <div class="desc-awkn">
      <div v-if="tabsSaveList.length<1">
        <div>
          <i class="el-icon-warning-outline"></i>
        </div>
        <div class="desc-toAdd">还未添加任何故障，快去添加吧~</div>
      </div>
      <div v-else class="select-tabs">
        <div class="tabs-list" v-for="(tabs,index) in tabsSaveList" :key="index">
          {{tabs.name}}
          <div class="close-i" @click="closeIcon(tabs,index)">
            <i class="el-icon-circle-close"></i>
          </div>
        </div>
      </div>
    </div>

    <div class="btm-desc" v-if="active===0">
      <div v-for="(port,index) in waterwayList" @click="handleSelect(port,index)" :class="{isSelsect:port.isSele===true}" :key="index">
        {{port.name}}
      </div>
    </div>

    <div class="btm-desc" v-if="active===1">
      <div v-for="(port,index) in wayList" @click="handleSelect(port,index)" :class="{isSelsect:port.isSele===true}" :key="index">
        {{port.name}}
      </div>
    </div>

    <div class="btm-desc" v-if="active===2">
      <div v-for="(port,index) in waterList" @click="handleSelect(port,index)" :class="{isSelsect:port.isSele===true}" :key="index">
        {{port.name}}
      </div>
    </div>

    <div class="save-btn">
      <el-button :block="true" @click="typeSavebtn" color="linear-gradient(to right, #FF6C60, #FE4D69)">保存</el-button>
    </div>
  </div>

</div>
</template>

<script>
export default {
  data() {
    return {
      username: '',
      show: false,
      actions: '',
      active: 0,
      fileList: [],
      tabList: [{
          key: 0,
          name: '绝不放弃'
        },
        {
          key: 1,
          name: '掉头发'
        },
        {
          key: 2,
          name: '的机会'
        }
      ],
      tabsSaveList: [],
      waterwayList: [{
          key: 0,
          name: '熬夜',
          isSele: false
        },
        {
          key: 1,
          name: '一点寒芒先到',
          isSele: false
        },
        {
          key: 2,
          name: '随后枪出游龙',
          isSele: false
        },
        {
          key: 3,
          name: '肥仔快乐水',
          isSele: false
        },
        {
          key: 4,
          name: '压力不稳',
          isSele: false
        },
        {
          key: 5,
          name: '无出水',
          isSele: false
        },
        {
          key: 6,
          name: '出水量太少',
          isSele: false
        },
      ],
      wayList: [{
          key: 0,
          name: '肥仔快乐水',
          isSele: false
        },
        {
          key: 1,
          name: '一点寒芒先到',
          isSele: false
        },
        {
          key: 2,
          name: '随后枪出游龙',
          isSele: false
        },
        {
          key: 3,
          name: '水枪出泡沫',
          isSele: false
        },
      ],
      waterList: [{
          key: 0,
          name: '碰头出水',
          isSele: false
        },
        {
          key: 1,
          name: '水枪出泡沫',
          isSele: false
        },
        {
          key: 2,
          name: '振动大',
          isSele: false
        },
      ]
    }
  },
  computed: {

  },
  methods: {
    handleType() {
      this.show = true
    },
    //问题类型保存
    typeSavebtn() {
      this.show = false
    },

    uploadImg() {},
    //tabs关闭icon事件
    closeIcon(row, index) {
      if (this.active === 0) {
        this.waterwayList.map((item) => {
          if (row.key === item.key) {
            item.isSele = !row.isSele
          }
        })
      } else if (this.active === 1) {
        this.wayList.map((item) => {
          if (row.key === item.key) {
            item.isSele = !row.isSele
          }
        })

      } else if (this.active === 2) {
        this.waterList.map((item) => {
          if (row.key === item.key) {
            item.isSele = !row.isSele
          }
        })

      }

      this.tabsSaveList.map((ele, eleIndex) => {
        if (row.key === ele.key) {
          this.tabsSaveList.splice(eleIndex, 1)
        }
      })
    },

    handleActive(row, index) {
      this.active = index
      this.tabsSaveList = []
    },
    //选中或者取消
    handleSelect(row, index) {
      this.waterwayList.map((item) => {
        if (row.key === item.key) {
          item.isSele = !row.isSele
        }
      })
      //
      if (this.tabsSaveList.length) {
        let isd;
        let ist;
        this.tabsSaveList.map((ele, eleIndex) => {
          if (row.key === ele.key) {
            this.tabsSaveList.splice(eleIndex, 1)
            isd = true
          } else {
            this.tabsSaveList.map((ele, eleIndex) => {
              isd = () => ele.key !== row.key
              ist = this.tabsSaveList.some(isd) //至少一个不等与
            })
            if (ist) {
              this.tabsSaveList.push(row)
            }
          }
        })
      } else {
        this.tabsSaveList.push(row)
      }
    }
  },
  watch: {
    active(newVal, oldVal) {

      if (newVal === 0) {
        waterwayList: [{
            key: 0,
            name: '熬夜',
            isSele: false
          },
          {
            key: 1,
            name: '一点寒芒先到',
            isSele: false
          },
          {
            key: 2,
            name: '随后枪出游龙',
            isSele: false
          },
          {
            key: 3,
            name: '肥仔快乐水',
            isSele: false
          },
          {
            key: 4,
            name: '压力不稳',
            isSele: false
          },
          {
            key: 5,
            name: '无出水',
            isSele: false
          },
          {
            key: 6,
            name: '出水量太少',
            isSele: false
          },
        ]
      }
      else if (newVal === 1) {
        this.wayList = [{
            key: 0,
            name: '肥仔快乐水',
            isSele: false
          },
          {
            key: 1,
            name: '一点寒芒先到',
            isSele: false
          },
          {
            key: 2,
            name: '随后枪出游龙',
            isSele: false
          },
          {
            key: 3,
            name: '水枪出泡沫',
            isSele: false
          },
        ]
      } else if (newVal === 2) {
        this.waterList = [{
            key: 0,
            name: '碰头出水',
            isSele: false
          },
          {
            key: 1,
            name: '水枪出泡沫',
            isSele: false
          },
          {
            key: 2,
            name: '振动大',
            isSele: false
          },
        ]
      }
    },
  }
}
</script>
