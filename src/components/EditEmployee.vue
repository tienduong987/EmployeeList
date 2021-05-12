<template>
  <div class="col-4">
        <form class="mb-5">
          <div class="form-group">
            <label for="fullName">Họ Tên</label>
            <input type="text" class="form-control" id="fullName" v-model='employee.fullName' />
          </div>
          <div class="form-group">
            <label for="titleName">Chức danh</label>
            <input type="text" class="form-control" id="titleName" v-model='employee.titleName' />
          </div>
          <div class="form-group">
            <label for="locationPathList">Đơn vị</label>
            <input type="text" class="form-control" id="locationPathList" v-model='employee.locationPathList'/>
          </div>
          <div class="btn btn-primary" @click="clickSave()" >Save</div>
        </form>
      </div>
</template>

<script>
export default {
    props:{
        employee:Object
    },
    methods:{
        clickSave(){
            this.$emit('save',this.employee)
        }
    }
}
</script>

<style>

</style>