<script lang="ts">

	

	let userInput: string;
	let paid:string;

    interface item {
        user: string;
        name: string;
        price: number;
    }

    let items: item[] = [];

    const validityCheck = (input): boolean => {
        let splitIn: string[] = input.split(" ");
        if (splitIn[0].length === 1 && Number(splitIn[2])) {
            return true;
        }

        return false;
    };

    const addItem = (input: string): void => {
        if (validityCheck(input)) {
            const splitInput = input.split(" ");

            let entry: item = {
                user: splitInput[0],
                name: splitInput[1],
                price: Number(splitInput[2]),
            };

            items = [...items, entry];
            userInput = "";
            document.getElementById("userinput").focus();
        } else {
            userInput = "";
        }
    };

    const onEnter = (e): void => {
        if (e.key === "Enter") {
            addItem(userInput);
        }
	};
	
	const paidUser = ():number=>{
		return 5
	}
</script>

<style>
</style>

<main>
    <h1>Grocery Splitter</h1>
    <h2>Entry</h2>
    <p>
        Format: "s itemName 42.42" 's' is reserved for shared items. Enter key
        adds the item.
    </p>
    <p>
        <input
            on:keyup={onEnter}
            id="userinput"
            placeholder="s item 42.42"
            bind:value={userInput}
			type="text" />
			<input bind:value={paid} maxlength="1" type="text" placeholder="Who paid?">
    </p>
	<h2>Display</h2>
	<p>
		{#if paid && items.length > 0}
		{paid} paid {paidUser()} 
		{/if}
		
	</p>
	


</main>
