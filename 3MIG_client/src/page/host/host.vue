<template>
    <div id="host">
    	<transition>
    		<router-view></router-view>
    	</transition>
    	<footer>
    		<router-link :class = "['footMenu-option', {'footMenu-onthis': footMenuFlag === index}]" v-for = '(option, index) in footMenuOption' tag = 'div' :to = 'option.toWhere' @click.native = 'toThis(index)'>
    			<img :src = 'option.optionImg'>
    			<span>{{ option.optionName }}</span>
    		</router-link>
    	</footer>
    </div>
</template>

<script>

import { mapState, mapActions } from 'vuex'

export default {
  	name: 'host',
  	data () {
  		return {
  			footMenuOption: [
  				{
  					optionName: '首页',
  					optionImg: require('../../assets/icon/home.svg'),
  					toWhere: '/host/home'
  				},
  				{
  					optionName: '分类',
  					optionImg: require('../../assets/icon/category.svg'),
  					toWhere: '/host/category'
  				},
  				{
  					optionName: '购物车',
  					optionImg: require('../../assets/icon/cart.svg'),
  					toWhere: '/host/cart'
  				},
  				{
  					optionName: '我的',
  					optionImg: require('../../assets/icon/user.svg'),
  					toWhere: '/host/user'
  				},
  			],
  			footMenuFlag: 0,
  		}
  	},

  	methods: {
  		toThis (index) {
  			this.footMenuFlag = index;
  		},
  		beginPosition () {
  			let url = window.location.href;
	  		let _position = url.split(`${window.location.host}/`)[1];
	  		switch (_position) {
	  			case 'host/home': this.footMenuFlag = 0;
	  			break;
	  			case 'host/category': this.footMenuFlag = 1;
	  			break;
	  			case 'host/cart': this.footMenuFlag = 2;
	  			break;
	  			case 'host/user': this.footMenuFlag = 3;
	  			break;
	  		}
  		}
  	},
  	
  	beforeMount () {
  		this.beginPosition();
  	},
}
</script>

<style scoped>
	footer {
		box-shadow: 0 -2px 10px #888888;
		background-color: #038950;
		position: fixed;
		z-index: 99;
		bottom: 0;
		width: 100%;
		height: 1.11rem;
		display: flex;
	}
	.footMenu-option {
		opacity: 0.3;
		padding-top: 0.14rem;
		display: flex;
		align-items: center;
		flex-direction: column;
		flex-grow: 1;
		text-align: center;
		transition: all 0.5s;
	}
	.footMenu-onthis {
		opacity: 1;
	}
	.footMenu-option img {
		width: 0.45rem;
		height: 0.45rem;
	}
	.footMenu-option span {
		color: white;
		letter-spacing: 2px;
		text-indent: 2px;
		font-size: 0.22rem;
		margin-top: 0.11rem;
	}
	/*.fade-enter {
		transform: translateX(0vh);
	}
	.fade-leave {
		transform: translateX(0px);
	}
	.fade-enter-active {
		transform: translateX(0px);
		transition: all 0.2s;
	}
	.fade-leave-active {
		transform: translateX(100px);
		transition: all 0.2s;
	}*/
</style>
