<template>
    <div class="container">
        <div class="headers">
            <h3>Tablero de tareas</h3>
        </div>
        <div class="container-columns">
            <div class="container-columns-column backlog" >
                <div class="container-columns-column-title">
                    Por hacer
                </div>
                <div class="container-columns-column-tasks backlog">
                    <draggable 
                        :list="backlog" :group="{ name: 'people' }" 
                        :animation="200" 
                        tag="div"
                        ghost-class="moving-card">
                        <transition-group type="transition" name="flip-list">
                            <div class="container-columns-column-tasks-task" v-for="task in backlog" :key="task.id">
                                <div class="container-columns-column-tasks-task-title">{{task.name}}</div>
                                <div class="container-columns-column-tasks-task-footer">
                                    <div class="container-columns-column-tasks-task-footer-date">{{task.date}}</div>
                                    <div class="container-columns-column-tasks-task-footer-priority">{{prioritys[task.priority]}}</div>
                                </div>
                            </div>
                        </transition-group>    
                    </draggable>
                </div>
            </div>
            <div class="container-columns-column inProgres" >
                <div class="container-columns-column-title">
                    En progreso
                </div>
                <div class="container-columns-column-tasks inProgres">
                    <draggable 
                        :list="inProgres" :group="{ name: 'people' }" 
                        :animation="200" 
                        tag="div"
                        ghost-class="moving-card">
                    <div class="container-columns-column-tasks-task" v-for="task in inProgres" :key="task.id">
                        <div class="container-columns-column-tasks-task-title">{{task.name}}</div>
                        <div class="container-columns-column-tasks-task-footer">
                            <div class="container-columns-column-tasks-task-footer-date">{{task.date}}</div>
                            <div class="container-columns-column-tasks-task-footer-priority">{{prioritys[task.priority]}}</div>
                        </div>
                    </div>
                    </draggable>
                </div>
            </div>
            <div class="container-columns-column review" >
                <div class="container-columns-column-title">
                    En revisión
                </div>
                <div class="container-columns-column-tasks review">
                    <draggable 
                        :list="review" :group="{ name: 'people' }" 
                        :animation="200" 
                        tag="div"
                        ghost-class="moving-card">
                    <div class="container-columns-column-tasks-task" v-for="task in review" :key="task.id">
                        <div class="container-columns-column-tasks-task-title">{{task.name}}</div>
                        <div class="container-columns-column-tasks-task-footer">
                            <div class="container-columns-column-tasks-task-footer-date">{{task.date}}</div>
                            <div class="container-columns-column-tasks-task-footer-priority">{{prioritys[task.priority]}}</div>
                        </div>
                    </div>
                    </draggable>
                </div>
            </div>
            <div class="container-columns-column finished" >
                <div class="container-columns-column-title">
                    Terminado
                </div>
                <div class="container-columns-column-tasks finished">
                    <draggable 
                        :list="finished" :group="{ name: 'people' }" 
                        :animation="200" 
                        tag="div"
                        ghost-class="moving-card">
                    <div class="container-columns-column-tasks-task" v-for="task in finished" :key="task.id">
                        <div class="container-columns-column-tasks-task-title">{{task.name}}</div>
                        <div class="container-columns-column-tasks-task-footer">
                            <div class="container-columns-column-tasks-task-footer-date">{{task.date}}</div>
                            <div class="container-columns-column-tasks-task-footer-priority">{{prioritys[task.priority]}}</div>
                        </div>
                    </div>
                    </draggable>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
import dataTasks from './tasks.json'
import draggable from "vuedraggable";
export default {
    components: {
        draggable
    },
    data() {
        return{
            backlog: dataTasks.filter(el => el.state === 1),
            inProgres: dataTasks.filter(el => el.state === 2),
            review: dataTasks.filter(el => el.state === 3),
            finished: dataTasks.filter(el => el.state === 4),
            columns: [
                {
                    key: 1,
                    name: 'Por hacer'
                },
                {
                    key: 2,
                    name: 'En progreso'
                },
                {
                    key: 3,
                    name: 'En revisión'
                },
                {
                    key: 4,
                    name: 'Terminado'
                },
            ],
            prioritys: {
                low: "Baja prioridad",
                medium: "Mediana prioridad",
                high: "Alta prioridad"
            }
        }
    }
}
</script>
<style lang="scss">
$colorBacklog: rgb(182, 42, 42);
$colorInProgres: #b43f11;
$colorReview: #947a07;
$colorFinished: #1e6e42;
.container{
    margin:0;
    padding:0;
    width: 100%;
    height: 100%;
    display: flex;
    // flex-wrap: wrap;
    flex-direction: column;
    &-columns{
        width: 100%;
        height: 100%;
        padding: 1%;
        display: flex;
        flex-direction: row;
        &-column{
            width: 20%;
            height: 90%;
            margin: 1% 1% 1% 1%;
            border-radius: 20px;
            padding: 1%;
            &.backlog { background-color: $colorBacklog; }
            &.inProgres { background-color: $colorInProgres; }
            &.review { background-color: $colorReview; }
            &.finished { background-color: $colorFinished; }
            &-title{
                width: 100%;
                height: 4%;
                // padding-top: 10px;
                color: white;
                // border-bottom: solid 1px #333;
            }
            &-tasks{
                width: 98%;
                height: 92%;
                padding: 2% 0% 0% 0%;
                // border: solid 3px red;
                &.backlog { background-color: lighten($colorBacklog, 15%); }
                &.inProgres { background-color: lighten($colorInProgres, 15%); }
                &.review { background-color: lighten($colorReview, 15%); }
                &.finished { background-color: lighten($colorFinished, 15%); }
                .flip-list-move {
                    transition: transform 0.5s;
                }
                &-task{
                    width: 92%;
                    height: 22%;
                    padding: 2%;
                    margin: 1% 0% 2% 1%;
                    background-color: #668bab;
                    border-radius: 10px;
                    color: white;
                    display: flex;
                    flex-direction: column;
                    &-title{
                        font-size: 1.5vw;
                        text-align: left;
                    }
                    &-footer{
                        margin-top: 5%;
                        width: 100%;
                        display: flex;
                        justify-content: flex-start;
                        flex-direction: row;
                        &-date{
                            width: 50%;
                            text-align: left;
                        }
                        &-priority{
                            width: 50%;
                            text-align: left;
                        }
                    }
                }
            }
        }
    }
}
</style>