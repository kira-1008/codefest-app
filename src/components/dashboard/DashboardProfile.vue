<template>
  <div :class="[$style.container, $style[$mq]]">
   
    <div :class="$style.profilehead">
      
        <div :class="$style.userinit">
        <div :class="[$style.arc ,$style.arc_start]"></div>
        <div :class="[$style.arc ,$style.arc_end]"></div>
        <p>{{ retrieveInitials }}</p>
        </div>
      
      <span :class="$style.username">{{ profile.name}}</span>
    </div>
    <hr :class="$style.rightHr" />
    <hr :class="$style.bottomHr"/>
    <div :class="$style.profile">
      <div :class="$style.about">
        <div :class="$style.wrapper">
        <div :class="[$style.countdiv, is_verified]">
          <div :class="$style.outside">
            <div :class="$style.inside">
          <span :class="$style.reftext"><p>Referral Count</p></span>
          <span :class="$style.refcount" v-if="profile.is_verified">
            {{profile.referral_count}}
          </span>
          <span :class="$style.refcount" v-else>
            <i class="far fa-times-circle"></i>
          </span>
            </div>
          </div>
          
        </div>  
        <div :class="$style.topdesign">
        <hr :class="$style.toprule"/>
        <div :class="$style.leftcircle"/>
        </div>
        <div :class="$style.bottom_left_design">
        <div :class="$style.outercircle"/>
        <div :class="$style.innercircle"/>
        <div :class="$style.verticalrule"/>
        </div>
        <div :class="$style.bottom_right_design">
          <hr :class="$style.rightbottomHr"/>
          <hr :class="$style.tiltedHr"/>
          <hr :class="$style.topHr"/>
          <div :class="$style.circle"/>
          </div>
        </div>
      
        <div :class="$style.box" v-if="profile.is_verified">
            <div :class="$style.bck">
            <div :class="$style.blck">
          <span :class="$style.value" v-if="['md', 'lg', 'xl', 'xxl'].includes(this.$mq)">
            <router-link :to="routerLocation" :class="$style.refcode">
              {{
              profile.referral_code
              }}
            </router-link>
          </span>
          <span v-else></span>
          <i class="fas fa-clipboard" :class="$style.copyIcon" @click="clickToCopy"></i>
          </div>
          </div>
        </div>
        <p :class="$style.helptext" v-if="profile.is_verified">
          Share the above referral link with your contacts to win exciting
          goodies!
        </p>
        <p :class="$style.disabledreferral" v-else>
          Referral link disabled. Please verify your account first and refresh
          the page.
          <br />
          <a href="javascript:void(0)" @click="resendVerification">Click here</a>
          to resend verification email.
        </p>
        
        <div :class="$style.profileinfo">
          <div :class="$style.row">
            <div :class="[$style.info_box,$style.left]">
              <div :class="$style.bck">
            <div :class="$style.blck">
              <div :class="$style.pkey">Name</div>
              <div :class="$style.pvalue">{{profile.name}}</div>
          </div>
          </div>
              </div>
               <div :class="[$style.info_box,$style.right]">
              <div :class="$style.bck">
            <div :class="$style.blck">
              <div :class="$style.pkey">Phone</div>
              <div :class="$style.pvalue">{{profile.phone}}</div>
          </div>
          </div>
              </div>
          </div>
           <div :class="$style.row">
            <div :class="[$style.info_box,$style.left]">
              <div :class="$style.bck">
            <div :class="$style.blck">
              <div :class="$style.pkey">Institute Name</div>
              <div :class="$style.pvalue">{{profile.institute_name}}</div>
          </div>
          </div>
              </div>
               <div :class="[$style.info_box,$style.right]">
              <div :class="$style.bck">
            <div :class="$style.blck">
              <div :class="$style.pkey">Email</div>
              <div :class="$style.pvalue">{{user_email}}</div>
          </div>
          </div>
              </div>
          </div>
           <div :class="$style.row">
            <div :class="[$style.info_box,$style.left]">
              <div :class="$style.bck">
            <div :class="$style.blck">
              <div :class="$style.pkey">Country</div>
              <div :class="$style.pvalue">{{profile.country}}</div>
          </div>
          </div>
              </div>
               <div :class="[$style.info_box,$style.right]">
              <div :class="$style.bck">
            <div :class="$style.blck">
              <div :class="$style.pkey">Resume(*.pdf)</div>
              <div :class="$style.pkey">
                <form enctype="multipart/form-data">
                
                <label :class="$style.fileInput"> 
                
                  Select file
                <input
                  type="file"
                  name="resume"
                  @change="
                    uploadResume($event.target.name, $event.target.files)
                  "
                />
                </label>
                <label id="fileName"></label>
                
              </form>
              </div>
          </div>
          </div>
              </div>
          </div>
          
          
          <div :class="$style.resume_helptext">
            <div :class="$style.bck">
              <div :class="$style.blck">
            <p>Resume upload is recommended to be considered for hiring
            opportunities!</p>
            </div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <div :class="$style.actionButtons">
      <div :class="$style.wrapper">
        <div :class="$style.top_design">
          <hr :class="$style.line">
          <div :class="$style.circle"></div>  
        </div>
      <div :class="$style.link" @click="$router.push('/profile/edit')">
      <div :class="$style.bck">
            <div :class="$style.blck">
        <span :class="$style.linkText">
          <h4>Edit Profile</h4>
        </span>
        </div>
            </div>
      </div>
      <div :class="$style.bottom_design">
        <hr :class="$style.down"> 
        <hr :class="$style.tilted">
        <hr :class="$style.top">
        <div :class="$style.circle"/>
      </div>
      </div>
      <div :class="$style.wrapper">
        
        <div :class="$style.top_design">
          <hr :class="$style.line">
          <div :class="$style.circle"></div>  
        </div>
           
      <div
        :class="$style.link"
        @click="$router.push('/password/change')"
       
      ><div :class="$style.bck">
            <div :class="$style.blck">
        <span :class="$style.linkText">
          <h4>Change Password</h4>
        </span>
        </div>
            </div>
      </div>
      <div :class="$style.bottom_design">
        <hr :class="$style.down"> 
        <hr :class="$style.tilted">
        <hr :class="$style.top">
        <div :class="$style.circle"/>
      </div>
      </div>
     
      <a v-if="!!certificate" :href="certificate" target="_blank">
         <div :class="$style.wrapper">
            <div :class="$style.top_design">
          <hr :class="$style.line">
          <div :class="$style.circle"></div>  
        </div>
        <div :class="$style.link">
           <div :class="$style.bck">
            <div :class="$style.blck">
          <span :class="$style.linkText">
            <h4>Get Certificate</h4>
          </span>
          </div>
            </div>
        </div>
        <div :class="$style.bottom_design">
        <hr :class="$style.down"> 
        <hr :class="$style.tilted">
        <hr :class="$style.top">
        <div :class="$style.circle"/>
      </div>
        </div>
      </a>
      
     
      <a v-if="!!resume" :href="resume" target="_blank">
         <div :class="$style.wrapper">
           <div :class="$style.top_design">
          <hr :class="$style.line">
          <div :class="$style.circle"></div>  
        </div>
        <div :class="$style.link">
          <div :class="$style.bck">
            <div :class="$style.blck">
          <span :class="$style.linkText">
            <h4>View Resume</h4>
          </span>
            </div>
            </div>
        </div>
        <div :class="$style.bottom_design">
        <hr :class="$style.down"> 
        <hr :class="$style.tilted">
        <hr :class="$style.top">
        <div :class="$style.circle"/>
      </div>
        </div>
      </a>
    </div>
  </div>
</template>

<script>
import { copyToClipboard } from "@js/utils";
import { SITE_URL } from "@js/constants";
import API from "@js/api";
import { auth } from "firebase/app";

const SectionLayout = () => import("@components/layouts/SectionLayout");
const ResponsiveTwoColumnLayout = () =>
  import("@components/layouts/ResponsiveTwoColumnLayout");

export default {
  components: {
    SectionLayout,
    ResponsiveTwoColumnLayout,
  },
  data() {
    return {
      certificate: null,
      resume: null,
      user_email: null
    };
  },
  computed: {
    retrieveInitials() {
      const { name } = this.profile;
      if (!name) return;
      const newName = name.split(/\s+/);
      if (newName.length > 1) return newName[0][0] + newName[1][0];
      return newName[0][0];
    },

    is_verified() {
      if (this.profile.is_verified == true) {
        return this.$style.verified;
      } else {
        return this.$style.notverified;
      }
    },

    routerLocation() {
      return {
        name: "~/login",
        query: {
          referral: this.profile.referral_code
        }
      };
    }
  },
  props: {
    profile: {
      required: true,
      type: Object
    }
  },
  created() {
    API.fetch("certificate/")
      .then(({ data }) => {
        this.$data.certificate = data.url;
      })
      .catch(e => {
        this.$data.certificate = null;
      });
    API.fetch("resume/")
      .then(({ data }) => {
        this.resume = data.resume;
      })
      .catch(e => {
        this.resume = null;
      });
    auth().onAuthStateChanged(user => {
      if (user) {
        this.user_email = user.email;
      }
    });
  },
  methods: {
    clickToCopy() {
      const referral = this.profile.referral_code;
      const referralShareLink = this.$router.resolve(this.routerLocation).href;
      copyToClipboard(`${SITE_URL}${referralShareLink}`);
      this.$toasted.global.success({
        message: `Copied "${referralShareLink}"!`
      });
    },
    resendVerification() {
      auth()
        .currentUser.sendEmailVerification()
        .then(() => {
          this.$toasted.global.success({
            message: "Verification Link has been sent."
          });
        })
        .catch(err => {
          this.$toasted.global.error_post({
            message: err.message
          });
        });
    },
    uploadResume(fieldName, fileList) {
      
      document.getElementById("fileName").innerHTML =fileList[0].name;
      console.log("hehehy");
      var resumeFile = new FormData();
      if (!fileList.length) return;
      resumeFile.append(fieldName, fileList[0], fileList[0].name);
      API.put("resume/", {
        body: resumeFile,
        headers: {
          "Content-Type": undefined
        }
      })
        .then(({ data }) => {
          const msg = "Your resume has been uploaded successfully!";
          this.$toasted.global.success({ message: msg });
          this.resume = data.resume;
        })
        .catch(err => {
          this.$toasted.global.error_post({ message: err.message });
        });
    }
  }
};
</script>

<style module lang="stylus">
@require '~@styles/anims';

.container {
  height: 100%;
  padding-top: 50px;

  .profilehead {
    height: 108px;
    display: flex;
    flex-direction: row;
    flex-wrap: nowrap;
    justify-content: space-between;
    align-items: center;

    
    .userinit {
      order: -2;
      
      border-radius: 50%;
      
      
      text-align: center;
      width: 110px;
      height: 110px;
      
      font: 48px 'Roboto Slab';
      font-weight: 700;
      color:$blue-tint;
    

      p {
        text-align: center;
        width: 100%;
        margin-top: 25px;
      }
    }
      .arc {
    order:-2;
    position:absolute;
    width:120px;
    height:120px;
    border-radius:100%;
    border:5px solid ;
}
      .arc_start {
        border-color:transparent transparent $blue-tint $blue-tint;
        transform: rotate(225deg);
      }
      .arc_end {
        border-color:transparent transparent $blue-tint $blue-tint;
       transform: rotate(-75deg);
      }

      ~/.xs ^[1..-1], ~/.sm ^[1..-1] {
        width: 72px;
        height: 72px;
        $font-size: 30px;
        padding: 12px;
      }
    

    .username {
      order: -1;
      color: $white;
      font-family: 'Roboto Slab';
      font-weight: 700;
      color: $blue-tint;
      text-align: right;
      $font-size: 50px;
      margin: 0;
      float: right;

      ~/.xs ^[1..-1], ~/.sm ^[1..-1] {
        $font-size: 36px;
      }
    }
  }

  hr {
    height: 6px;
    background-color: $blue-tint;
    display: block;
    width: 50%;
    
 
    border: none;
  }

  .rightHr {
    margin-top:-20px;
    
    margin-left:50%;

    ~/.xs ^[1..-1], ~/.sm ^[1..-1] {
      margin-bottom: 16px;
    }
  }
  .bottomHr {
      width:35%;
      height:1px;
      margin-top:8px;
    margin-bottom: 72px;
    margin-left: 65%;

    ~/.xs ^[1..-1], ~/.sm ^[1..-1] {
      margin-bottom: 16px;
    }
  }

  .actionButtons {
    margin: 40px auto;
    text-align: center;
    display:flex;
    flex-flow:row;
    justify-content: space-around;

    .wrapper{
      position:relative;
        height:100px;
        width:300px;
       

      .top_design{
          .line{
            position:absolute;
            left:180px;
            height:2px;
            background-color:$blue-tint;
            width:120px;
          }
          .circle{
            position:absolute;
            left:300px;
            top:-8px;
            height:20px;
            width:20px;
            border-radius:50%;
            border:2px solid $blue-tint;
          }
      }
      .bottom_design{
        .down{
            position:absolute;
            height:2px;
            left:120px;
            width:132px;
        }
        .tilted{
          position:absolute;
          transform:rotate(-45deg);
          width:60px;
          left:242px;
          height:2px;
          bottom:24px;
        }
        .top{
          position:absolute;
            height:2px;
            left:293px;
            bottom:45px;
            width:40px;
        }
        .circle{
          position:absolute;
            left:332px;
            bottom:35px;
            height:20px;
            width:20px;
            border-radius:50%;
            border:2px solid $blue-tint;
        }
      }
    }

      

  }

  .link {
    position:relative;
    
    margin: 10px 10px;
  
    height:70px;
    width: 260px;
    padding: 18px;
    background-color:$blue-tint;
    text-align: center;
    cursor: pointer;
    display: inline-block;
    clip-path: polygon(10% 0, 100% 0, 100% 62%, 90% 100%, 0 100%, 0 38%);

    .bck{
        position:absolute;
        top:1px;
        left:1px;
        right:1px;
        bottom:1px;
        clip-path: polygon(10% 0, 100% 0, 100% 62%, 90% 100%, 0 100%, 0 38%);
        background:$mystic;
    }
    .blck{
        position:absolute;
        top:1px;
        left:1px;
        right:1px;
        bottom:1px;
        clip-path: polygon(10% 0, 100% 0, 100% 62%, 90% 100%, 0 100%, 0 38%);
        background: radial-gradient(circle, rgba(7, 249, 254, 0.2), rgba(7, 249, 254, 0.1));
       
    }

    .linkText {
     color:$blue-tint;
     display:inline;
      

      h4 {
        font-family: 'Roboto Slab';
        $font-size: 22px;
        margin-top:15px;
        
      }
    }

    
    ~/.xs ^[1..-1], ~/.sm ^[1..-1] {
      margin-bottom: 30px;
    }
  }

  .profile {
    display: flex;
    flex-direction: row;
    justify-content: space-around;

    .about {
      postion:relative;
      text-align: center;
      margin: 15px;
      width: 100%;
      
      .wrapper{
        position:relative;
        text-align:center;
        height: 300px;
        width:300px;  
        margin: auto;
        margin-top: 0px;
        margin-bottom: 50px;
        border:2px solid transparent;
      }
      .topdesign
      {
        
        .toprule{
          height:2px; 
          position:absolute;
          top:40px;
          left:200px;
          width:100px;
          background: $blue-tint;
        }
        .leftcircle{
          position:absolute;
          top:31px;
          left:300px;
          height:20px;
          width:20px;
          border-radius:50%;
          border:2px solid $blue-tint;
        }
      }
      .bottom_left_design
      {
        
          .outercircle{
          position:absolute;
          top:260px;
          left:20px;
          height:32px;
          width:32px;
          border-radius: 50%;
          border:3px solid $blue-tint;
        }
        .innercircle{
          position:absolute;
          top:268px;
          left:27px;
          height:17px;
          width:17px;
          border-radius: 50%;
          background:rgba(7,249,255,0.5);
        }
        .verticalrule{
          position:absolute;
          height:50px;
          width:12px;
          top:212px;
          left:28px;
          background:rgba(7,249,255,0.5);
        }
      }
      .bottom_right_design{
        
        .rightbottomHr{
          
          position:absolute;
          height:2px;
          width:32px;
          top:290px;
          left:166px;
          background:$blue-tint;
        }
        .topHr{
          position:absolute;
          height:2px;
          width:32px;
          top:212px;
          left:275px;
          background:$blue-tint;
        }
        .tiltedHr{
          position:absolute;
          height:2px;
          width:110px;
          top:251px;
          left:182px;
          background:$blue-tint;
          transform:rotate(-45deg)
        }
        .circle{
          position:absolute;
          top:203px;
          left:307px;
          height:20px;
          width:20px;
          border-radius:50%;
          border:2px solid $blue-tint;
        }
      }
      
      
      .box {
          position:relative;
          height:60px;
          width:380px;
          background-color:$blue-tint;
          margin:auto;
          
          clip-path: polygon(5% 0, 100% 0, 100% 62%, 95% 100%, 0 100%, 0 38%);
          

        .bck{
          position:absolute;
          
          clip-path: polygon(5% 0, 100% 0, 100% 62%, 95% 100%, 0 100%, 0 38%);
          background-color:$mystic;
          left:1px;
          top:1px;
          bottom:1px;
          right:1px;
        }
        .blck{
          position:absolute;
          left:1px;
          top:1px;
          bottom:1px;
          right:1px;
          color:$blue-tint;
          align-content: center;
        
          clip-path: polygon(5% 0, 100% 0, 100% 62%, 95% 100%, 0 100%, 0 38%);
          background:radial-gradient(circle, rgba(7, 249, 254, 0.2), rgba(7, 249, 254, 0.1));

        }

       


        .copyIcon {
          padding: 12px;
          cursor: pointer;
          margin-right: 15px;
          float: right;
        }
        

        ~/.lg ^[1..-1], ~/.xxl ^[1..-1], ~/.xl ^[1..-1], ~/.md ^[1..-1] {
          /*.key {
            display: inline-block;
            float: left;
            font-weight: 700;
            font-family: 'Roboto Slab';
            $font-size: 24px;
            padding: 10px 15px 10px;
            height: 100%;
            color: $white;
            border-radius: inherit;
            border-bottom-right-radius: 0;
            border-top-right-radius: 0;
            border-right: 1px solid $vermilion;
            background: alpha($vermilion, 0.7);
          }
          */

          .value {
            display: inline-block;
            $font-size: 18px;
            font-family: 'Roboto Slab';
            font-weight: 600;
            padding: 12px;
            height: 100%;
            margin-left:15%;
            .refcode{
              color:$blue-tint;
            }
          }
        }

        ~/.md ^[1..-1] {
          width: 100%;
          margin-left: 0%;
        }

        ~/.xs ^[1..-1], ~/.sm ^[1..-1] {
          display: flex;
          flex-flow: column;
          width: 200px;
          height: 200px;
          margin: auto;

          /*.key {
            display: inline-block;
            width: 100%;
            font-weight: bold;
            font-family: 'Roboto Slab';
            $font-size: 24px;
            padding: 8px 15px;
            color: var(--text-color);
          }
          */

          .copyIcon {
            width: 100%;
            $font-size: 60px;
            padding: 24px 0;
            color: $blue-tint;
          }
        }
      }
    }

    .helptext {
      $font-size: 14px;
      display: inline-block;
      border: 3px solid $blue-tint;
      border-radius: 10px;
      padding: 8px 16px;
      margin-top: 40px;
      color:$blue-tint;
      /*box-shadow: var(--small-icon-shadow);*/
    }

    .disabledreferral {
      display: inline-block;
      $font-size: 14px;
      box-shadow: 0 0 20px red inset;
      border: 1px solid red;
      border-radius: 10px;
      padding: 8px 16px;
    }

    .countdiv {
      position:relative;
      height: 230px;
      width:230px;  
      margin: auto;
      margin-top:50px;
      display: flex;
      flex-flow:column;
     
      background:$blue-tint;
      clip-path: polygon(100% 0, 100% 70%, 70% 100%, 0 100%, 0 0);
      .outside{
        position: absolute;
	      top:1px;
	      left: 1px;
        right: 1px;
        bottom: 1px;
	      background: $mystic;
       
      
        clip-path: polygon(100% 0, 100% 70%, 70% 100%, 0 100%, 0 0);
      }
      .inside {
        position: absolute;
        top: 1px;
        left: 1px;
        right: 1px;
        bottom: 1px;
         display: flex;
      flex-flow:column nowrap; 
        background: radial-gradient(circle, rgba(7, 249, 254, 0.2), rgba(7, 249, 254, 0.1));
        clip-path: polygon(100% 0, 100% 70%, 70% 100%, 0 100%, 0 0);
        
        .reftext {
          order: 0;
        height: 50px;
        vertical-align:bottom;
        color:$blue-tint;
        /*color: var(--text-color);*/
        padding: 15px 0;
        font: 600 20px 'Roboto Slab';
       }

        .refcount {
          vertical-align:text-top;
          height: 100px;
         
        order: 1;

  
        font: 500 100px 'Roboto Slab';
        color: $blue-tint;
        }
      }
      
    }

    .verified {
      border: 2px solid $blue-tint;
      /*animation: timeline-border-green 1s ease-in-out infinite alternate;*/
    }

    .notverified {
      border: 5px solid red;
      animation: timeline-border-white 1s ease-in-out infinite alternate;

      i {
        color: red;
      }
    }

    .profileinfo {
      
      margin: auto;

      .row {
        position:relative;
        
        height 100px;
        width:90%;
        margin:auto; 
        margin-top: 20px;
        margin-bottom: 20px;
        $font-size: 16px;
        display: flex;
        flex-direction: row;
        text-align: center;
         flex-wrap: nowrap;
        justify-content: space-between;
      align-items: center;

        .left{
          order:-2;
          
        }
        .right{
          float:right;
          margin:0;
          order:-1;
          
        }
        .info_box {
          position:relative;
          height:70px;
          width:380px;
          background-color:$blue-tint;
          
          
          clip-path: polygon(5% 0, 100% 0, 100% 62%, 95% 100%, 0 100%, 0 38%);
          

        .bck{
      position:absolute;
          
          clip-path: polygon(5% 0, 100% 0, 100% 62%, 95% 100%, 0 100%, 0 38%);
          background-color:$mystic;
          left:1px;
          top:1px;
          bottom:1px;
          right:1px;
        }
        .blck{
          position:absolute;
          left:1px;
          top:1px;
          bottom:1px;
          right:1px;
          color:$blue-tint;
          display:flex;
          flex-flow:column;
          align-items:center;
          clip-path: polygon(5% 0, 100% 0, 100% 62%, 95% 100%, 0 100%, 0 38%);
          background:radial-gradient(circle, rgba(7, 249, 254, 0.2), rgba(7, 249, 254, 0.1));
          
        }
        
        .pkey{
          font: 600 15px 'Roboto Slab';
          margin-top:5px;
          width:100%;
        
        input[type="file"] {
          display: none !important;
        }

        .fileInput {
          
          position:relative;
          padding:3px;
          border:1px solid $blue-tint;
          cursor: pointer;
          font-weight:100;
          
        }
          
        }

        .pvalue {
          width:100%;
          order: 2;
           font: 600 23px 'Roboto Slab';
          
          
        }

        }
      }
      

      .resume_helptext{
         position:relative;
          height:70px;
          width:90%;
          margin:auto;
          background-color:$blue-tint;
          font: 500 20px 'Roboto Slab';
          
          
          clip-path: polygon(2% 0, 100% 0, 100% 62%, 98% 100%, 0 100%, 0 38%);
        .bck{
          position:absolute;
          
          clip-path: polygon(2% 0, 100% 0, 100% 62%, 98% 100%, 0 100%, 0 38%);
          background-color:$mystic;
          left:1px;
          top:1px;
          bottom:1px;
          right:1px;
        }
        .blck{
          position:absolute;
          left:1px;
          top:1px;
          bottom:1px;
          right:1px;
          color:$blue-tint;
          display:flex;
          flex-flow:column;
          align-items:center;
          clip-path: polygon(2% 0, 100% 0, 100% 62%, 98% 100%, 0 100%, 0 38%);
          background:radial-gradient(circle, rgba(7, 249, 254, 0.2), rgba(7, 249, 254, 0.1));

          
        }
      }

      ~/.xs ^[1..-1], ~/.sm ^[1..-1] {
        .row {
          position:relative;
        height 100px;
        width:90%;
        margin:auto; 
        margin-top: 20px;
        margin-bottom: 20px;
        $font-size: 16px;
        display: flex;
        flex-direction:column;
        flex-wrap: nowrap;
        justify-content: center;
        align-items: center;
         
          $font-size: 12px;
          .left{
            margin:auto;
          }
          .right{
            margin:auto;
          }

          .pkey {
            order: 1;
            width: 100%;
          }

          .pvalue {
            order: 2;
            width: 100%;
          }
        }
        .resume_helptext{
          height:100px;
        }
      }

      ~/.xs ^[1..-1] {
        width: 240px;
      }

      ~/.sm ^[1..-1] {
        width: 300px;
      }

      ~/.md ^[1..-1] {
        width: 550px;
      }
    }
  }
}
</style>
