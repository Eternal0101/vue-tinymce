<template>
    <div>
        <TreeChart :json="treeData" />
    </div>
</template>
<script>
    import TreeChart from "vue-tree-chart";
    export default{
        name:'tree',
        components: {
            TreeChart
        },
        data(){
            return {
                treeData:{
                    name: 'root',
                    image_url: "https://fuss10.elemecdn.com/e/5d/4a731a90594a4af544c0c25941171jpeg.jpeg",
                    children: [
                        {
                            name: 'children1',
                            image_url: "https://fuss10.elemecdn.com/e/5d/4a731a90594a4af544c0c25941171jpeg.jpeg"
                        },
                        {
                            name: 'children2',
                            image_url: "https://fuss10.elemecdn.com/e/5d/4a731a90594a4af544c0c25941171jpeg.jpeg",
                            mate: {
                                name: 'mate',
                                image_url: "https://fuss10.elemecdn.com/e/5d/4a731a90594a4af544c0c25941171jpeg.jpegg"
                            },
                            children: [
                                {
                                    name: 'grandchild',
                                    image_url: "https://fuss10.elemecdn.com/e/5d/4a731a90594a4af544c0c25941171jpeg.jpeg"
                                },
                                {
                                    name: 'grandchild2',
                                    image_url: "https://fuss10.elemecdn.com/e/5d/4a731a90594a4af544c0c25941171jpeg.jpeg"
                                },
                                {
                                    name: 'grandchild3',
                                    image_url: "https://fuss10.elemecdn.com/e/5d/4a731a90594a4af544c0c25941171jpeg.jpeg"
                                }
                            ]
                        },
                        {
                            name: 'children3',
                            image_url: "https://fuss10.elemecdn.com/e/5d/4a731a90594a4af544c0c25941171jpeg.jpeg"
                        }
                    ]
                }
            }
        }
    }
</script>
