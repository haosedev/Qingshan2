<template>
    <div>
        <group title="号牌查询，使用 search + result">

        </group>
        <div>
            <card>
                <div slot="content" class="version-padding center version">
                    <p>
                        <img class="logo" src="../assets/h-logo.png">
                    </p>
                    <p>Version:{{version}}</p>
                </div>
            </card>
        </div>
    </div>
</template>

<script>
import {
    Group,
    Cell,
    Card
} from 'vux'
export default {
    components: {
        Group,
        Cell,
        Card
    },
    name: 'hello',
    data() {
        return {
            msg: 'Welcome',
            version: '0.1.12',
        }
    }
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