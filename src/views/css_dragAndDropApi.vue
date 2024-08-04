<template>
    <div class="container" ref="container">
        <div class="left" data-drop="move">
            <div v-for="(course, index) in courses" :key="course.name" :style="{ background: course.background }"
                data-state="copy" draggable="true" class="classify">
                {{ course.name }}
            </div>
        </div>
        <div class="right">
            <h1>课程表</h1>
            <table>
                <thead>
                    <tr>
                        <th class="white"></th>
                        <th>星期1</th>
                        <th>星期2</th>
                        <th>星期3</th>
                        <th>星期4</th>
                        <th>星期5</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="row in 7" :key="row">
                        <template v-if="row === 1">
                            <td :rowspan="4" data-drop="copy">上午</td>
                            <td v-for="col in 5" :key="col" data-drop="copy"></td>
                        </template>
                        <template v-else-if="row === 2 || row === 3 || row === 4">
                            <td v-for="col in 5" :key="col" data-drop="copy"></td>
                        </template>
                        <template v-else-if="row === 5">
                            <td :rowspan="3" data-drop="copy">下午</td>
                            <td v-for="col in 5" :key="col" data-drop="copy"></td>
                        </template>
                        <template v-else>
                            <td v-for="col in 5" :key="col" data-drop="copy"></td>
                        </template>
                    </tr>
                </tbody>
            </table>
        </div>
        <div class="add-classify">
            <input v-model="newCourse" type="text" placeholder="输入课程+班级" />
            <button @click="addCourse">添加课程班级</button>
        </div>
    </div>
</template>

<script setup>
import { ref, onMounted, reactive } from 'vue';

const courses = ref([
    { name: '语文', background: 'blue' },
    { name: '数学', background: 'green' },
    { name: '英语', background: 'pink' },
    { name: '体育', background: 'red' }
]);
const newCourse = ref('');
const container = ref(null);
let source = null;

const addCourse = () => {
    if (newCourse.value.trim().length) {
        courses.value.push({
            name: newCourse.value,
            background: randomColor()
        });
        newCourse.value = '';
    }
};
const randomColor = () => {
    return '#' + Math.random().toString(16).substring(2, 8);
};

const deepParentNode = (node) => {
    while (node) {
        if (node.dataset && node.dataset.drop) {
            return node;
        }
        node = node.parentNode;
    }
};

onMounted(() => {
    container.value.addEventListener('dragstart', (e) => {
        e.dataTransfer.effectAllowed = e.target.dataset.state;
        source = e.target;
    });

    container.value.addEventListener('dragover', (e) => {
        e.preventDefault();
    });

    container.value.addEventListener('dragenter', (e) => {
        const conMoveCopy = deepParentNode(e.target);
        if (!conMoveCopy) return;
        document.querySelector('.can-move')?.classList.remove('can-move');
        conMoveCopy.classList.add('can-move');
    });

    container.value.addEventListener('drop', (e) => {
        document.querySelector('.can-move')?.classList.remove('can-move');
        const conMoveCopy = deepParentNode(e.target);
        if (!conMoveCopy) return;

        if (source.dataset.state == 'copy' && conMoveCopy.dataset.drop == 'copy') {
            const cloneNode = source.cloneNode(true);
            cloneNode.dataset.state = 'move';
            conMoveCopy.innerHTML = '';
            conMoveCopy.append(cloneNode);
        }
        if (source.dataset.state == 'move' && conMoveCopy.dataset.drop == 'copy') {
            conMoveCopy.innerHTML = '';
            conMoveCopy.append(source);
        }
        if (source.dataset.state == 'copy' && conMoveCopy.dataset.drop == 'move') {
            return;
        }
        if (source.dataset.state == 'move' && conMoveCopy.dataset.drop == 'move') {
            source.remove();
        }
    });

    window.addEventListener('selectstart', (e) => e.preventDefault());
});
</script>

<style scoped>
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box
}

h1 {
    text-align: center;
}

.container {
    width: 1000px;
    margin: auto;
    display: flex;
    justify-content: space-between;
}

.left {
    width: 120px;
    height: auto;
    border: 1px solid rgba(0, 0, 0, 0.2);
    overflow-y: auto;
    margin-right: 10px;
}

.right {
    flex: 1;
}

.left::-webkit-scrollbar {
    width: 5px;
    color: red;

}

.left::-webkit-scrollbar-thumb {
    background: #888;
}

.left::-webkit-scrollbar-thumb:hover {
    background: #555;
    /* 颜色 */
}

.left::-webkit-scrollbar-track {
    background: #f1f1f1;
}


.left .classify {
    margin-top: 20px;
}

.left .classify:last-child {
    margin-bottom: 20px;
}

.classify {
    width: 80px;
    height: 40px;
    line-height: 38px;
    text-align: center;
    border: 1px solid rgba(0, 0, 0, 0.2);
    margin: auto;
    background: white;
    font-size: 18px;
    color: white;
}

table {
    margin-left: 20px;
    border-collapse: collapse;
}

tr,
td,
th {
    border: 1px solid rgba(0, 0, 0, 0.2);
}

td {
    width: 120px;
    height: 70px;
}

.can-move {
    background-color: rgba(0, 0, 0, 0.2);
}

.add-classify {
    margin: auto;
    width: 150px;
    height: 150px;
    display: flex;
    flex-direction: column;
    justify-content: space-evenly;
    align-items: center;
}

.add-classify input {
    height: 40px;
    width: 120px;
    padding-left: 8px;
    font-size: 16px;
}

.add-classify button {
    height: 40px;
    width: 120px;
}

.white {
    border: none;
    background: none;
}
</style>