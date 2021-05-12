<template>
  <div id="app" class="container">
    <hr />
    <div>
      <h3 style='text-align:center ' class="mb-5">Quản lý nhân sự</h3>
      <div class="btn btn-info btn-block mb-3" @click='clickAdd()' >ADD</div>
    </div>
    <div class="row">
      <div class="col">
        <table class="table">
          <thead>
            <tr>
              <th>#</th>
              <th>NHÂN VIÊN</th>
              <th>CHỨC VỤ</th>
              <th>ĐƠN VỊ</th>
              <th>THAO TÁC</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(employee,index) in employeeList" :key="index">
              <th>{{ employee.id }}</th>
              <td>{{ employee.fullName }}</td>
              <td>{{ employee.titleName }}</td>
              <td>{{ employee.locationPathList }}</td>
              <td>
                <div class="btn-group">
                  <div class="btn btn-danger" @click='clickEdit(employee)' >Edit</div>
                  <div class=" btn btn-warning" @click='clickDelete(employee)'>Delete</div>
                </div>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
        <EditEmployee :employee='employee' @save='clickSave' v-if='isEdit'/>
    </div>
  </div>
</template>

<script>



import EditEmployee from './components/EditEmployee'
// import { v4 as uuidv4 } from 'uuid';
export default { 
  name: 'App',
  components:{
    EditEmployee
  },
  data(){
    
    return{
      
        employeeList:[
                {
                  id: 1,
                  fullName: "Đặng Tiến Dương",
                  titleName: "FrontEnd Intern",
                 locationPathList: "Văn phòng Hà Nội",
                },
                {
                  id: 2,
                  fullName: "Nguyễn Văn B",
                  titleName: "BackEnd Intern",
                 locationPathList: "Văn phòng Hà Nội",
                },
                {
                  id: 3,
                  fullName: "Nguyễn Thị C",
                  titleName: "FrontEnd Develop",
                 locationPathList: "Văn phòng Hà Nội",
                },
                {
                  id: 4,
                  fullName: "Cao Văn D",
                  titleName: "FrontEnd Devolop",
                 locationPathList: "Văn phòng HCM",
                },
                {
                  id: 5,
                  fullName: "Trần Quốc E",
                  titleName: "FrontEnd Intern",
                 locationPathList: "Văn phòng HCM",
                },
           
        ],
        employee:null,
        isEdit:false,
        
        
    }
     
  },
  mounted() {
    var dataString =localStorage.getItem('employeeList')
    // this.employeeList = JSON.parse(localStorage.getItem('employeeList'))
    if(dataString){
      this.employeeList=JSON.parse(dataString)
    }else{
      this.employeeList=[]
    }
  },

  methods:{
    clickAdd(){
      
      let employee ={
        id: Math.floor(Math.random() * 100000000),
        fullName: "",
        titleName: "",
        locationPathList: "",
      }
      this.employee=employee,
      this.isEdit =!this.isEdit
    },
    clickSave(employee){
      var index= this.employeeList.findIndex(item => item.id === employee.id)
      if(index >=0){
        this.employeeList.splice(index,1,employee)
        localStorage.setItem( 'employeeList',JSON.stringify(this.employeeList))
      }else{
        this.employeeList.push(employee)
       localStorage.setItem( 'employeeList',JSON.stringify(this.employeeList))
      }
     localStorage.getItem('employeeList');
      this.isEdit=false
    },
    clickEdit(employee){
      this.employee =JSON.parse(JSON.stringify(employee)) ,
      this.isEdit=true
    },
    clickDelete(employee){
      var index = this.employeeList.findIndex(item => item.id === employee.id)
      this.employeeList.splice(index,1)
      localStorage.setItem( 'employeeList',JSON.stringify(this.employeeList))
    }
    },
    
  }      


</script>

<style></style>
