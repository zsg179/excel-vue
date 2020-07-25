<template>
    <div>
        <input type="text" v-model="key">
        <a href="javascript:void(0)" @click="download">导出</a>
    </div>
</template>

<script>
export default {
    data(){
        return{
            key: ""
        }

    },
    methods: {
        download() {
            this.$axios({
                method:"post",
                url:"/download",
                data:{
                    key:this.key
                },
                responseType: 'blob'
            }).then(res => {
                const link = document.createElement('a')
                const blob = new Blob([res.data], { type: 'application/vnd.ms-excel' })
                link.style.display = 'none'
                link.href = URL.createObjectURL(blob)
                link.setAttribute('download', "深圳个账表.xls")
                document.body.appendChild(link)
                link.click()
                document.body.removeChild(link)
            })

        }
    }
}
</script>