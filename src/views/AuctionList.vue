<template>
  <section>
    <section v-if="getAuctionListSuccess">
      <section
        v-if="auctionList.length"
        id="list"
        class="auction-list"
      >
        <section
          v-for="auction in auctionList"
          :key="auction.aid"
          class="auction-item"
        >
          <section class="pic">
            <img
              :src="auction.thumbnail"
              alt=""
            >
          </section>
          <section class="desc">
            <p class="title">
              <a href="#">{{ auction.name }}</a>
            </p>
            <p class="detail">
              {{ auction.detail }}
            </p>
            <p class="other">
              <span>类型：<i>{{ auction.type }}</i></span>
              <span>估值：<i>￥{{ auction.price }}</i></span>
            </p>
          </section>
        </section>
      </section>
      <section
        v-else
        id="noData"
        class="tips"
      >
        对不起，当前没有可以竞买的拍品
      </section>
    </section>

    <section
      v-else
      id="serverError"
      class="tips"
    >
      服务异常，请稍后再试
    </section>
  </section>
</template>

<script>
import { mapState } from "vuex";

export default {
  name: "AuctionList",
  computed: mapState({
    auctionList: (state) => state.auctionList,
    getAuctionListSuccess: (state) => state.getAuctionListSuccess,
  }),
  created() {
    this.getAuctionList();
  },
  methods: {
    getAuctionList() {
      this.$store.dispatch("getAuctionList");
    },
  },
};
</script>

<style lang="less">
.auction-list {
  width: 100%;
  padding: 20px;
  box-sizing: border-box;
  .auction-item {
    width: 100%;
    margin-bottom: 20px;
    padding-bottom: 15px;
    border-bottom: 1px dashed grey;
    display: flex;
    flex-direction: row;
    .pic {
      width: 30%;
      height: 180px;
      overflow: hidden;
      display: flex;
      justify-content: center;
      img {
        width: 100%;
        height: auto;
      }
    }
    .desc {
      flex: 1;
      margin-left: 20px;

      .title {
        font-size: 18px;
      }
      .detail {
        overflow: hidden;
        text-overflow: ellipsis;
        display: -webkit-box;
        -webkit-line-clamp: 3;
        -webkit-box-orient: vertical;
      }
      .other {
        span {
          margin-right: 20px;
        }
        i {
          font-style: normal;
        }
      }
    }
  }
}
.tips {
  width: 100%;
  height: 500px;
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
