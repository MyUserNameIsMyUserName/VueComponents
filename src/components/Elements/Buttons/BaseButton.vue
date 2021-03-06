<template>
  <button class="baseButton" :class="[this.btnSize, ('icon_pos_'+this.btnIconPos), this.hoverAnim, inAnim]"  v-bind:style="styleObject">
    <font-awesome-icon :icon="['fas', btnIcon]" v-bind:style="iconStyleObj" />
    <p class="btnMsg">
      {{ msg }}
    </p>
  </button>
</template> 

<script>
import { library } from '@fortawesome/fontawesome-svg-core'
import { fas } from '@fortawesome/free-solid-svg-icons'
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome'

library.add( fas );

export default {
  name: "BaseButton",
  props: {
    msg: String,
    color: String,
    backColor: String,
    size: String,
    rounded: String,
    icon: String,
    iconPos: String,
    iconBack: String,
    hoverAnim: String,
    inAnim: String
  },
  components: {
      FontAwesomeIcon
  },
  data() {
    return {
      styleObject: {
        backgroundColor: "#03A9F4",
        color: "white",
        borderRadius: 0,
      },
      iconStyleObj: {
        backgroundColor: "transparent",
      },
      btnSize : "medium",
      btnIcon: null,
      btnIconPos: null,
    }
  },
  methods: {
      assignColor : function() {
          switch(this.size) {
            case 'xs':
                this.btnSize = 'extraSmall';
                break;
            case 's':
                this.btnSize = 'small';
                break;
            case 'm':
                this.btnSize = 'medium';
                break;
            case 'l':
                this.btnSize = 'large';
                break;
            case 'xl':
                this.btnSize = 'extraLarge';
                break;
            default:
                // code block
                this.btnSize = 'medium';
            }
      }
  },
  created(){
      if (this.color != undefined){
          this.styleObject.color = this.color;
      };
      if (this.backColor != undefined){
          this.styleObject.backgroundColor = this.backColor;
      };
      if (this.size != undefined){
          this.assignColor();
      }
      if (this.rounded == "true"){
          this.styleObject.borderRadius = '2em';
          //this.styleObject.padding = '0.25em .75em';
      }
      if (this.icon != undefined){
          this.btnIcon = this.icon;
      }

      if(this.iconPos != undefined) {
          this.btnIconPos = this.iconPos;
      }
      if(this.iconBack != undefined){
          this.iconStyleObj.backgroundColor = this.iconBack;
      }
  }  
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
    button.baseButton {
        border: none;
        position: relative;
        overflow: hidden;
        cursor: pointer;
        transition: 0.1s linear all;
        box-shadow: 0 0px 5px rgba(0,0,0,0.25);
        height: max-content;
        display: flex;
        flex-direction: row;
        align-items: center;

        &:before{
            content: " ";
            position: absolute;
            display: flex;
            width: 100%;
            height: 100%;
            z-index: 0;
            top: 0;
            left:0;
        }

        &:hover {
            box-shadow: 0 3px 10px rgba(0,0,0,0.5);
            transition: 0.2s linear all;

            &:before {
                background: rgba(0,0,0,0.1);
            }
        }

        &:focus {
            outline: none;
        }

        &:active {
            box-shadow: 0 0px 2.5px rgba(0,0,0,0.5);
            transition: 0.025s linear all;

            &:before {
                background: rgba(0,0,0,0.2);
            }
        }

        p.btnMsg {
            padding: 0;
            margin: 0;
            pointer-events: none;
            z-index: 10;
            padding: 0.25em .5em;
            line-height: 1;
        }

        svg {
            padding: 0.25em .5em;
        }
    }

    button.baseButton.flyOutText:not(.icon_pos_right) {
        
        p {
            animation: flyOutText 3s;
            animation-fill-mode: forwards;
        }
    }

    button.baseButton.icon_pos_right {
            flex-direction: row-reverse;    
    }

    button.baseButton.flyOutText.icon_pos_right {

        p {
            animation: flyOutTextRight 3s;
            animation-fill-mode: forwards;
        }
    }

    @keyframes flyOutText {
      from { opacity: 0; margin-left: -100%; }
      to { opacity: 1; margin-left: 0%; }
    }

    @keyframes flyOutTextRight {
      from { opacity: 0; margin-right: -100%; }
      to { opacity: 1; margin-right: 0%; }
    }

    button.baseButton.growText {

        svg {
            border-radius: 50%;
            width: 1em;
            height: 1em;
            padding: 0.25em;
            animation: inGrowSVG 5s;
            animation-fill-mode: forwards; 
        }

        p {
            animation: inGrowText 5s;
            animation-fill-mode: forwards; 
        }
    }

    @keyframes inGrowText {
      0% { opacity: 0; width: 0; font-size: 0; margin: 0 -.25em; overflow: hidden;}
      50% { opacity: 0; width: 0; font-size: 0; margin: 0 -.25em; overflow: hidden;}
      100% { opacity: 1; margin: 0; overflow: hidden;}
    }

    @keyframes inGrowSVG {
      0% { transform: rotate(0deg) }
      50% { transform: rotate(0deg)}
      100% { transform: rotate(360deg) }
    }

    .baseButton.flyOutIcon {

        svg {
            width: 1em;
            margin-left: -2em;
            color: transparent;
            transition: 0.15s ease all;
        }

        &:hover svg{
            margin-left: 0;
            color: white;
            transition: 0.35s ease all;
        }
    }   

    .extraSmall {
        font-size: .5em;
    }

    .small {
        font-size: .75em;
    }

    .medium {
        font-size: 1em;
    }

    .large {
        font-size: 1.5em;
    }

    .extraLarge {
        font-size: 2em;
    }
</style>
