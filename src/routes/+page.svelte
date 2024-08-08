 <script lang="ts">
	
   import DivideIcon from '$lib/icons/DivideIcon.svelte';
   import X_Icon from '$lib/icons/X_Icon.svelte';
   import DeleteIcon from '$lib/icons/DeleteIcon.svelte';
   import SubtractionIcon from '$lib/icons/SubtractionIcon.svelte';
   import PlusIcon from '$lib/icons/PlusIcon.svelte'
   import EquaLIcon from '../lib/icons/EquaLIcon.svelte';

   function addToEquation(value:string){
      equation += value;

   }
   function backSpace (){
      switch (equation.substring(equation.length-3,equation.length)){
         case " + ":
         case " - ":
         case " * ":
         case " / ":
             equation = equation.substring(0, equation.length - 3);
             break;
         default:
             equation = equation.substring(0, equation.length - 1);
            }
            }

   function clear(){
      equation = "";
   }
   function solve(){
      try{
        let answer = eval(equation);
        if (answer == undefined) throw SyntaxError;
        equation = answer;
      }

       catch (error){
         let output = document.getElementById('output');
         output?.classList.add('bg-red-600');
         setTimeout(() => {
            output?.classList.remove('bg-red-600');
         } , 500 );
      }


   }

  let equation: string = "";

  function onKeyDown(){
   console.log('hi');
  }
     
 </script>


 <svetle:head>
    <title>
       calculator
    </title>
 </svetle:head>

 <!-- svelte-ignore a11y-no-static-element-interactions -->
 <svelte:window on:keydown|preventDefault={onKeyDown}/>


<!--padding لتعديل  حجم الحاوية-->
 <div class="  bg-[#bec4d5]   h-fit rounded-3xl grid grid-cols-4 gap-2 p-8 text-lg font-semibold shadow-2xl w-[18rem]" > <!--هذا الحاوية الاب-->



 <!--خانة الارقام-->
 <div 
 id="output"
 class="bg-[#dfe3f1] text-end rounded-3xl  col-span-4 min-h-14
  flex  items-center px-5 mb-3 shadow-xl break-all transition-all "> {equation} </div>

   <button on:click={() => clear()} class="bg-[#990033] hover:bg-[#990033]/80 text-lg ">AC</button> <!--مسح الكل-->

   <button on:click={() => addToEquation(' / ')} class="bg-[#5e626e]" > <DivideIcon/> </button> 

   <button on:click={() => addToEquation(' * ')} class="text-sm bg-[#5e626e]"> <X_Icon/> </button> 

   <button on:click={() => backSpace( ) } class="bg-[#990033] hover:bg-[#990033]/80  text-2xl "> <DeleteIcon/> </button> 

   <button on:click={() => addToEquation('7')}>7</button>
   <button on:click={() => addToEquation('8')}>8</button>
   <button on:click={() => addToEquation('9')}>9</button>

   <button on:click={() => addToEquation(' - ')} class="bg-[#5e626e]">  <SubtractionIcon/> </button> 

   <button on:click={() => addToEquation('4')}>4</button>
   <button on:click={() => addToEquation('5')}>5</button>
   <button on:click={() => addToEquation('6')}>6</button>

   <button on:click={() => addToEquation(' + ')} class="text-lg bg-[#5e626e]"> <PlusIcon/>  </button> 

   <button on:click={() => addToEquation('1')}>1</button>
   <button on:click={() => addToEquation('2')}>2</button>
   <button on:click={() => addToEquation('3')}>3</button>


   <button  on:click={() => addToEquation(' /100 ')} class="bg-[#5e626e]">%</button>

   <button on:click={() => addToEquation('.')}>.</button>
   <button on:click={() => addToEquation('0')}>0</button>
   
   

   <button on:click={() => solve()} class="text-2xl col-span-2 "> <EquaLIcon/> </button>

  
 </div>


