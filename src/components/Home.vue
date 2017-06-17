<template>
    <div>
        <search @result-click="resultClick" @on-change="getResult" :results="results" v-model="value" position="absolute" auto-scroll-to-top
            top="46px" @on-focus="onFocus" @on-cancel="onCancel" @on-submit="onSubmit" ref="search"></search>
        <group>

        </group>
        <div>
            <card>
                <div slot="content" class="version-padding center version">
                    <p>
                        <img class="logo" src="../assets/h-logo.png">
                    </p>
                    <p>Version:{{ version }}</p>
                </div>
            </card>
        </div>
    </div>
</template>

<script>
    import {
        Group,
        Cell,
        Card,
        Search
    } from 'vux';
    import XLSX from 'xlsx';
    export default {
        components: {
            Group,
            Cell,
            Card,
            Search,
        }, methods: {
            setFocus() {
                this.$refs.search.setFocus();
            },
            resultClick(item) {
                window.alert('you click the result item: ' + JSON.stringify(item))
            },
            getResult(val) {
                this.results = val ? getResult(this.value) : []
            },
            onSubmit() {
                this.$refs.search.setBlur()
                this.$vux.toast.show({
                    type: 'text',
                    position: 'top',
                    text: 'on submit'
                })
            },
            onFocus() {
                console.log('on focus');
                var filename = '../assets/test.xlsx';
                //尝试读取xlsx
                var read_opts = { type: 'binary' };
                //var read_opts = { type: 'base64' };
                const workbook = XLSX.read(filename, read_opts);
                // 获取 Excel 中所有表名
                const sheetNames = workbook.SheetNames; // 返回 ['sheet1', 'sheet2']
                console.log(sheetNames);
                // 根据表名获取对应某张表
                const worksheet = workbook.Sheets[sheetNames[0]];
                console.log(worksheet);
                //const aa = XLSX.utils.sheet_to_json(worksheet);
                //console.log(aa);
            },
            onCancel() {
                console.log('on cancel')
            }
        },
        name: 'Home',
        data() {
            return {
                results: [],
                version: '0.1.18',
            }
        }
    }
    function getResult(val) {
        let rs = []
        for (let i = 0; i < 20; i++) {
            rs.push({
                title: `${val} result: ${i + 1} `,
                other: i
            })
        }
        return rs
    }

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    .version-padding {
        padding: 20px 10px 10px 10px;
    }

    .center {
        text-align: center;
    }

    .version {
        color: #ccc;
    }
</style>