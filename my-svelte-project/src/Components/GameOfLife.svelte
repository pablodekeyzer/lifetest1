<script lang="ts">
    import Cell from "./Cell.svelte";

    let length = 200
 let width = 200
 let gameData = [
     [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
     [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
     [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
     [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
     [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
     [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
     [0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0],
     [0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0],
     [0, 0, 0, 0, 0, 0, 1, 1, 1, 0, 0, 0, 0, 0, 0],
     [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
     [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
     [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
     [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
     [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
     [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0]
 ];
    function handleClick(event) {
        console.log(event)
           // gameData[i][j] === 0 ? gameData[i][j] = 1: gameData[i][j] = 0

    }
 function nextFrame() {
     let alivecells = []
     //calculate result
     for (let  rownr = 0; rownr <gameData.length; rownr++){
         let row = gameData[rownr]
         for (let columnnr = 0; columnnr <row.length; columnnr++){
             let cell = row[columnnr]
             if (checkDOA(cell, rownr, columnnr, gameData)){
                 alivecells.push([rownr,columnnr])
                 console.log('alive')
             }
         }
     }
     console.log(alivecells)
     //reset all original data
     gameData = [
         [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
         [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
         [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
         [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
         [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
         [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
         [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
         [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
         [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
         [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
         [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
         [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
         [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
         [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
         [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0]
     ];
     //insert new result
     console.log(gameData)
     for (const cell of alivecells){
         gameData[cell[0]][cell[1]] = 1
     }
     console.log(gameData)
 }
 function checkDOA(cell, rownr, columnnr, gameData){
     let neighbors = countNeighbors(rownr, columnnr, gameData)
     console.log(neighbors)
     if (cell && (neighbors===2|| neighbors===3)){
        return true
     }
     else if (!cell && neighbors===3)
         return true
     else
     return false
 }
 function countNeighbors(rownr, columnnr, gameData){
     let neighbors = [
         [rownr-1, columnnr+1,],
         [rownr-1,columnnr],
         [rownr-1,columnnr-1],
         [rownr,columnnr+1],
         [rownr,columnnr-1],
         [rownr+1,columnnr+1],
         [rownr+1,columnnr],
         [rownr+1,columnnr-1]
     ]
     let output: number = 0
     for( let neighbor of neighbors){
         if (isReal(neighbor[0], neighbor[1],gameData)){
             output += gameData[neighbor[0]][neighbor[1]]
         }
     }
     return output
 }
 function isReal(rownr, columnnr, gameData){
     return !(rownr < 0 || columnnr < 0 || rownr >= gameData.length || columnnr >= gameData[0].length);
 }
</script>

<div>
    <div class="raster">
        { #each gameData as row,i}
            <div class="row">
                { #each row as cell,j}
                    <Cell alive={cell} c={i} r={j} on:click="{handleClick()}"/>
                {/each}
            </div>
        {/each}
    </div>
    <button on:click={nextFrame}>Next</button>
</div>

<style>
    .raster {
        margin-top: 1vh;
        width: 100rem;
        height: 95vh;
        border: solid black 1px;
        align-items: center;
    }
    .row {
        display: flex;
        flex-direction: row;
        width: 100%;

    }

</style>
