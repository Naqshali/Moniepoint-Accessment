<template>
  <div>
    <div class="nav-container">
      <div class="navbar">
        <div>
          <img src="../assets/img/ramos.png" alt="Icon" />
        </div>
        <div class="list">
          <ul>
            <li>Dashboard</li>
            <li>Reports</li>
            <li>Documents</li>
            <li>History</li>
            <li>Settings</li>
          </ul>
        </div>
        <div>
          <button class="nav-btn">Sign Up</button>
        </div>
      </div>
    </div>
    <div class="main-container">
      <div class="TopHeading">
        <h1>
          <img src="../assets/img/headicon.png" alt="Icon" />
          Analytics <br />
          that <span>Helps </span>you
        </h1>
        <div class="Video">
          <img src="../assets/img/video.png" alt="Icon" />
        </div>
      </div>
      <h1 class="Shape">
        shape
        <img src="../assets/img/graph.png" alt="Icon" />
        the future
      </h1>
    </div>
    <div class="center-section-bg">
      <div class="container">
        <div class="center-section">
          <div class="top">
            <div>
              <h2>
                Your key to strategic <br />
                sucess through analytics
              </h2>
            </div>
            <div>
              <h4>
                Ready for exciting, instantaneous, <br />
                all- accessible insights in real time?
              </h4>
            </div>
          </div>
          <div class="center">
            <div class="center-left">
              <div class="left-section">
                <button id="setting-reports" class="btn-primary fade-in">
                  Setting up reports
                </button>
                <div class="para">
                  <h2>
                    Fast and easy access <br />
                    to analytics
                  </h2>
                  <p>
                    One platform is a comprehensive system of solutions that
                    will be the first step towards the dignitation of you
                    business
                  </p>
                </div>
              </div>
              <div class="right-section">
                <h4>Sales statistics</h4>
                <div class="visitors">
                  <div class="sales">
                    <img src="../assets/img/sales.png" alt="Icon" />
                    <span>
                      <span>Total Profit</span> <br />
                      <strong class="total-profit-value">$ 264.2K</strong>
                    </span>
                  </div>
                  <div class="bar-section">
                    <span> Visitors </span>
                    <div class="progress-container">
                      <div
                        class="progress-bar"
                        :style="{ width: progress + '%' }"
                      ></div>
                    </div>
                    <!-- <div class="progress-bar">
                      <span class="progress-bar-fill"></span>
                    </div> -->
                    <div class="visitors-value">
                      <div ref="countup">
                        <strong>
                          <CountUp
                            :key="counterKey"
                            :endVal="56"
                            :start="countUpOptions.start"
                            :end="countUpOptions.end"
                            :options="countUpOptions"
                          />K</strong
                        >
                      </div>
                      <div class="visitors-up">
                        <img src="../assets/img/visitors-up.png" alt="Icon" />
                      </div>
                    </div>
                  </div>
                </div>
                <div class="line-graph">
                  <h5>Visit Statistics</h5>
                  <div class="statistics">
                    <img src="../assets/img/semi-graph.png" alt="Icon" />
                    <div class="rate">
                      <span class="rate-title">Rate</span>
                      <span>
                        <i class="gg-arrow-top-right-o"></i>
                      </span>
                      <div class="rate-value">
                        +
                        <CountUp
                          :key="counterKey"
                          :endVal="58"
                          :start="countUpOptions.start"
                          :end="countUpOptions.end"
                          :options="countUpOptions"
                        />
                        %
                      </div>
                    </div>
                  </div>
                </div>
              </div>
            </div>
            <div class="center-right">
              <div class="transactions">
                <div class="base transactions-move-left">
                  <img
                    class="animated-arrow"
                    id="arrow"
                    src="../assets/img/transaction-img1.png"
                    alt="Icon"
                  />
                  <div class="people">
                    <img
                      src="../assets/img/transaction-prople.png"
                      alt="Icon"
                    />
                  </div>
                </div>
                <div
                  class="transactions-value base transactions-move-right"
                  id="myDiv"
                >
                  <span class="title"> Transactions </span><br />
                  <div class="up">
                    <img src="../assets/img/transaction-up.png" alt="Icon" />
                  </div>
                  <span>
                    <div class="value" ref="countup">
                      <CountUp
                        :key="counterKey"
                        :endVal="47"
                        :start="countUpOptions.start"
                        :end="countUpOptions.end"
                        :options="countUpOptions"
                      />K
                    </div>
                  </span>
                </div>
              </div>
              <div class="widget-control">
                <h3>Widget Control</h3>
                <p>
                  Reports provide a comprehensive overview of important aspects
                  of web analytics
                </p>
              </div>
            </div>
          </div>
        </div>
      </div>
      <div class="last-section">
        <div><h4>Up to</h4></div>
        <div class="analysis-value">45%</div>
        <div class="para">
          <p>
            <strong>
              Incrase your analytics effeciency upto 45%. Unique <br />
              algorithms provice insights from data reduce time for analysis
              <br />
              and save time for making important informed decisions.
            </strong>
          </p>
        </div>
      </div>
    </div>
    <div style="height: 100px"></div>
  </div>
</template>

<script>
import CountUp from "vue-countup-v2";
export default {
  name: "HelloWorld",
  props: {
    msg: String,
  },
  components: {
    CountUp,
  },
  data() {
    return {
      progress: 0,
      intervalId: null,
      isVisible: false,
      counterKey: 0,
      countUpOptions: {
        start: 0,
        duration: 5,
      },
    };
  },
  mounted() {
    window.addEventListener("scroll", this.handleScroll);
    this.checkVisibility();
    this.updateProgress();
  },
  beforeDestroy() {
    window.removeEventListener("scroll", this.handleScroll);
  },
  methods: {
    handleScroll() {
      if (!this.checkVisibility()) {
        this.counterKey++;
        this.animateTransactionsBlock();
        this.progress = 0;
        this.animateTransactionImg();
        this.settingsButtonAnimation();
      }
    },
    checkVisibility() {
      // This function check if a div is visible on screen at the moment or not
      const element = this.$refs.countup;
      if (!element) return false;
      const rect = element.getBoundingClientRect();

      const isVisible =
        rect.top >= 0 &&
        rect.left >= 0 &&
        rect.bottom <=
          (window.innerHeight || document.documentElement.clientHeight) &&
        rect.right <=
          (window.innerWidth || document.documentElement.clientWidth);

      return isVisible;
    },
    updateProgress() {
      // This is a progress bar value return function
      this.intervalId = setInterval(() => {
        if (this.progress < 56) {
          this.progress += 10;
        }
      }, 500);
    },
    animateTransactionsBlock() {
      // This function to re-animate img with class 'animated-arrow'
      var divs = document.querySelectorAll("div");
      divs.forEach(function (div) {
        div.style.animation = "none";
        div.offsetHeight;
        div.style.animation = null;
      });
    },
    animateTransactionImg() {
      // This function to re-animate img with class 'animated-arrow'
      const arrow = document.getElementById("arrow");
      arrow.classList.remove("animated-arrow");
      void arrow.offsetWidth;
      arrow.classList.add("animated-arrow");
    },
    settingsButtonAnimation() {
      // This function to re-animate img with class 'fade in'
      const arrow = document.getElementById("setting-reports");
      arrow.classList.remove("fade-in");
      void arrow.offsetWidth;
      arrow.classList.add("fade-in");
    },
  },
};
</script>

<style scoped lang="scss">
.iCountUp {
  font-size: 12em;
  margin: 0;
  color: #4d63bc;
}
</style>
