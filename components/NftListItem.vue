<template>
    <div>
        <div class="cover-image">
            <picture>
                <source :srcset="getImage(parseNftMetaData(nft.metadata).image)" type="image/webp">
                <img class="big-image" :src="getImage(parseNftMetaData(nft.metadata).image)" alt="">
            </picture>
            <div v-if="like" class="content-text">
                <div class="btn-like-click">
                    <div class="btnLike">
                        <input type="checkbox" checked>
                        <i class="ri-heart-3-line"></i>
                    </div>
                </div>
            </div>
            <div class="user-text">
                <div class="user-avatar">
                    <!-- <picture>
                        <source srcset="~/assets/images/avatar/10.webp" type="image/webp">
                        <img class="sm-user" src="~/assets/images/avatar/10.jpg" alt="">
                    </picture> -->
                    <span>{{ parseNftMetaData(nft.metadata).name }}</span>
                </div>
                <!-- <div v-if="floorPrice" class="number-eth">
                    <span class="main-price">{{ floorPrice }} ETH</span>
                    <span>(${{ convertToUsd() }})</span>
                </div> -->
            </div>
        </div>
    </div>
</template>


<script>
export default {
  name: 'NftListItem',
  props: {
    nft: {
      type: Object,
      required: true
    },
    like: {
        type: Boolean,
    }
  },
  data() {
      return {
          floorPrice: null,
      }
  },
  mounted() {
    if(this.like) this.nft.like = true
  },
  methods: {
    parseNftMetaData(value) {
        return JSON.parse(value)
    },
    getImage(value) {
       if(value && value != undefined ) return ( value.includes('ipfs://ipfs')) ? value.replace('ipfs://ipfs','https://ipfs.moralis.io:2053/ipfs/') : value.replace('ipfs://','https://ipfs.moralis.io:2053/ipfs/')
       return ''
    },
    getNftFloorPrice() {
        this.$axios.get('https://sea-turtle-app-n8fhg.ondigitalocean.app' + this.nft.token_address)
            .then( (data)  => {
                if(data.data) {
                    this.floorPrice = this.convertToEthPrice(data.data.data.price)
                }
            })
            .catch( (error)  => {
                console.log(error);
            })
    },
    convertToEthPrice(value) {
        return (parseInt(value)/1000000000000000000).toFixed(3)
    },
    convertToUsd() {
        return 405.64 * this.floorPrice
    }
  }
}
</script>