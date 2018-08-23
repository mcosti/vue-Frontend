<template>

    <div id="header" :style="{marginTop: this.alertsHeight}">
        <!--<img src="public/WebDollar-logo-black.png" id="logo"/>-->

        <div class="topnav" id="menu">

            <a href="#" id="logoBox" class="active logoMenu" :class="this.mobileMenuOpened && this.isMobile ? 'openedMenuLink' : '' ">
                <img v-on:click="this.collapseMenuBack" src="/public/assets/images/WebDollar-logo-white.png" alt="webDollar logo" id="logo" title="webDollar logo"/>
            </a>
			<!--</router-link>
			 <div><a class="copyPoolLink" @click="copyToClipboard"> Copy {{this.poolReferralFee}} % Referral Link </a> </div> -->
          <!--  <div>  <a href="https://exchange.webdron.com" target="_blank">Exchange</a>         </div> -->
           <div>  <a href="https://webdron.com" target="_blank">WEBDRON Home</a>         </div>
            


            <a href="javascript:void(0);" style="font-size:15px;" :style="{display: (mobileMenuOpened || isMobile==false) ? 'none':'block'}" class="icon showMenu" @click="this.showMobileMenu" :class="mobileMenuOpened ? 'openedMenuLink' : '' ">&#9776;</a>

        </div>
        <div id="WebDollarAlertsStickyBar"></div>
    </div>

</template>

<script>



    export default {

        name: "HeaderLayout",

        components: {
        },

        data () {
            return {
                screenWidth: 0,
                alertsHeight: 0,
                mobileMenuOpened: false,
                isMobile: false,
                alerts: [
                    {
                        message: 'test text'
                    },{
                        message: 'test text 2'
                    }
                ]
            }
        },

        methods:{

            collapseMenuBack(){

                this.mobileMenuOpened = false;

            },

            showMobileMenu() {

                this.mobileMenuOpened = true;

            },

            verifyIfIsMobile(){

                if (this.screenWidth<768){

                    this.isMobile=true;

                }else{

                    this.isMobile=false;

                }

            },

            addEvent (object, type, callback) {
                if (object === null || typeof(object) === 'undefined') return;
                if (object.addEventListener) {
                    object.addEventListener(type, callback, false);
                } else if (object.attachEvent) {
                    object.attachEvent("on" + type, callback);
                } else {
                    object["on"+type] = callback;
                }
            }

        },

        mounted(){

            if (typeof window === 'undefined') return;

            this.addEvent(window, "resize", (event) => {

                this.screenWidth = window.innerWidth;
                this.verifyIfIsMobile();

            });

            this.addEvent(window, "scroll", (event) =>{

                if (this.mobileMenuOpened==true){
                    this.mobileMenuOpened=false;
                }

            });

            this.screenWidth = window.innerWidth;
            this.verifyIfIsMobile();

        }

    }
</script>