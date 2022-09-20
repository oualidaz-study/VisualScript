<script lang="ts">
import { defineComponent } from 'vue'
    export default defineComponent({
        /**
         *  returns data
         */
        data() {
            /**
             *  return positions of client and the movement
             */
            return {
                positions: {
                    clientX: 0,
                    clientY: 0,
                    movementX: 0,
                    movementY: 0
                }
            }
        },
        /**
         * 
         */
        methods: {
            /**
             * 
             * @typeParam event - MouseEvent 
             * 
             */
            onMouseDown: function (event: MouseEvent) {
                event.preventDefault()
                // get the mouse cursor position at startup:
                this.positions.clientX = event.clientX
                this.positions.clientY = event.clientY
                document.onmousemove = this.onMouseDrag
                document.onmouseup = this.onMouseUp
            },
            /**
             * 
             * @param event 
             */
            onMouseDrag: function (event: MouseEvent) {
                event.preventDefault()
                this.positions.movementX = this.positions.clientX - event.clientX
                this.positions.movementY = this.positions.clientY - event.clientY
                this.positions.clientX = event.clientX
                this.positions.clientY = event.clientY
                // set the element's new position:
                this.$refs.node.style.top = (this.$refs.node.offsetTop - this.positions.movementY) + 'px'
                this.$refs.node.style.left = (this.$refs.node.offsetLeft - this.positions.movementX) + 'px'
            },
            /**
             * 
             */
            onMouseUp () {
                document.onmouseup = null
                document.onmousemove = null
            }
        }
    })
</script>

<template>
    <!--Node-->
    <div ref="node" id="node" @mousedown="onMouseDown">
        <!--Name of the node (NOT FOR OPERATORS)-->
        <p id="node-label"> ADD </p>
        
        <!--Actual part of the node-->
        <div id="components">
            <!--Inputs (TODO AUTO GENERATION!!!)-->
            <div id="connection-array">
                <button id="connection-buttons" />
                <button id="connection-buttons" />
            </div>  
            <!--Operator Label (NOT FOR FUNCTIONS)-->
            <p id="operation-label">+</p>
            <!--Inputs (TODO AUTO GENERATION!!!)-->
            <div id="connection-array">
                <button id="connection-buttons" />
            </div>
        </div>
    </div>  
</template>
  
<style scoped>
    #node {
      display: flex;
      flex-direction: column;
      border-radius: 25px;
      background:darkslategrey;
      padding: 5px;
      width: 200px;
      height: min-content;
      align-items: stretch;
      position: relative;
      cursor: move;

    }
  
    #node-label {
      margin: 0px;
      text-align: center;
      
      background-color: lightseagreen;
      border-radius: 25px 25px 0 0;
    }
  
    #components {
      display: flex;
      padding: 5px;
    }
  
    #operation-label {
      color: white;
      text-align: center;
      align-self: center;
      flex-grow: 1;
      font-size: 50px;
    }
  
    #connection-array {
      display: flex;
      flex-direction: column;
      justify-content: space-around;
    }
  
    #connection-buttons {
      height: 20px;
      width: 20px;
      padding: 1px;
      border-color: white;
      background-color: lightseagreen;
      border-radius: 50%;
    }
</style>