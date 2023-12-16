<template>
  <section class="content">
    <div class="container-fluid">
      <div class="row mainname">
        <p class="location">{{ location }}  {{ name }}</p>
      </div>
    <div class="row main">
          <div class="col-lg-3 col-6 bottom">
            <!-- small box -->
            <div class="small-box bg-info card">
              <div class="inner">
                <span>CONVEYOR BELT</span>
              </div>
              <div class="icon1">
                <a href="#"><img class="icon2" src="/img/icon/belt.png" alt="" title=""></a>
              </div>
             
            </div>
          </div>
          <!-- ./col -->
          <div class="col-lg-3 col-6 bottom">
            <!-- small box -->
            <div class="small-box bg-success card">
              <div class="inner">
                <span>IT</span>
                
              </div>
              <div class="icon1">
                <a href="#"><img class="icon2" src="/img/icon/it.png" alt="" title=""></a>
              </div>
            </div>
          </div>
          <!-- ./col -->
          <div class="col-lg-3 col-6 bottom">
            <!-- small box -->
            <div class="small-box bg-warning card">
              <div class="inner">
                <span>ELECTRICAL</span>

                
              </div>
              <div class="icon1">
                <a href="#"><img class="icon2" src="/img/icon/elec.png" alt="" title=""></a>
              </div>
              
            </div>
          </div>
          <!-- ./col -->
          <div class="col-lg-3 col-6 bottom">
            <!-- small box -->
            <div class="small-box bg-danger card">
              <div class="inner">
                <span>AIR CONDITIONER</span>

                
              </div>
              <div class="icon1">
                <a href="#"><img class="icon2" src="/img/icon/air.png" alt="" title=""></a>
              </div>
              
            </div>
          </div>
          <!-- ./col -->
        </div>
   </div>
  </section>
   
</template>
  
  <script>
import * as signalR from "@microsoft/signalr";

export default  {
    data() {
      return {
        pat: '',
        location: '', // Tên danh mục (lấy từ params)
        name: '', // Tên danh mục (lấy từ params)
      products: [] // Danh sách sản phẩm tương ứng với danh mục
      };
    },

    created() {
    this.location = this.$route.params.counters; 
    this.name = this.$route.params.counter; 
    console.log(this.location+"  "+this.name);
  },

    mounted() {
    this.hubConnection = new signalR.HubConnectionBuilder()
    .withUrl('https://localhost:7030/chatHub')
    .configureLogging(signalR.LogLevel.Information)
    .build();

  this.hubConnection.start().then(() => {
    console.log("SignalR connection");
    this.recivedmessage();
    }).catch(err => console.error("Signalr Connection failed start:", err));
    },
    methods: {
    recivedmessage() {
      this.hubConnection.on("ReceiveMessage", (data, message) => {
      console.log(data+message);
      }); 
    }, 
    handleChange() {
      this.hubConnection.invoke("SendMessageFromClient", this.category, this.category1).catch(function (err) {
        return console.error(err.toString());
    });
    },
    }
    
};
</script>

<style>
.row.main {
    margin-top: 7px;
}
span {
    color: white;
    font-weight: 700;
    font-size: 16px;
}
.row.mainname {
    justify-content: center;
    margin-top: 30px;
}
p.location {
    color: #2c3790;
    font-size: 38px;
    font-weight: bold;
}
.bottom {
    margin-bottom: 0px;
    margin-top: 12px;
}
.card {
    display: flex;
    align-items: center;
    height: 180px;
}
img.icon2 {
    height: 80%;
    margin-top: 5%;
}
</style>