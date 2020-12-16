<template>
  <v-card>
      <v-flex xs12 sm10>
        <v-tree url="/item/category/list"
                :isEdit="isEdit"
                @handleAdd="handleAdd"
                @handleEdit="handleEdit"
                @handleDelete="handleDelete"
                @handleClick="handleClick"
        />
      </v-flex>
  </v-card>
</template>

<script>
  export default {
    name: "category",
    data() {
      return {
        isEdit:true
      }
    },
    methods: {
      handleAdd(node) {
        console.log("add .... ");
        console.log(node);
     /*   this.$http.get("/item/category/addCategory",{
          params:{
            node
          }
        })*/
       this.$http.get("/item/category/addCategory",{
          params:{

           name: node.name,
            parentId: node.parentId,
            isParent: node.isParent,
            sort: node.sort
          }
        }).then(function (oubs) {
          if (oubs.data==1){
            alert("添加成功")
          } else {
            alert("添加失败")
          }

        })
      },
      handleEdit(id, name,obj) {
        console.log("edit... id: " + id + ", name: " + name)
        this.$http.get("/item/category/updateCategory",{
          params:{
             id:id,
            name: name,
             parentId: obj.parentId,
             isParent: obj.isParent,
             sort: obj.sort
          }
        }).then(function (oubs) {
          if (oubs.data==1){
            alert("修改失败")

          } else {
            alert("修改成功")
          }

        })



      },
      handleDelete(id) {
        console.log("delete ... " + id)
        this.$http.get("/item/category/deleteCategory/"+id).then({

        })
        console.log("delete ... " + id)
      },
      handleClick(node) {
        console.log(node)
      }
    }
  };
</script>

<style scoped>

</style>
