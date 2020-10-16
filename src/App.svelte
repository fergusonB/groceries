<script lang="ts">



    let userInput: string;
    let paid: string;

    interface item {
        user: string;
        name: string;
        price: number;
    }
    interface user {
        name: string;
        total: number;
    }

    let items: item[] = [];
    let users: user[] = [];

    const onEnter = (e): void => {
        if (e.key === "Enter") {
            addUser(userInput);
            addItem(userInput);
        }
    };

    const validityCheck = (input:string): boolean => {
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
			
	
		
			updateUser(entry)



            userInput = "";
            document.getElementById("userinput").focus();
        } else {
            userInput = "";
        }
	};
	
	const updateUser = (entry:item):void=>{
		for (const ea of users){
				if (entry.user === ea.name){
					ea.total+=entry.price
				}
			}
			
	}

    const addUser = (input: string): void => {
        if (validityCheck(input)) {

            let user: user = {
                name: input[0],
                total: 0,
			};
			
			let userFound = false
			for (const each of users){
				if (each.name === user.name){
					userFound =true
				}
			}
			if (! userFound ) users = [...users,user]
			



        }
        
    };

    const calcUser = (user: string): number => {
        let amount: number = 0;
        for (const ea of items) {
            if (ea.user === user) {
                amount += ea.price;
            }
        }
        return amount;
    };
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
        <input
            bind:value={paid}
            maxlength="1"
            type="text"
            placeholder="Who paid?" />
    </p>
    <h2>Display</h2>
    <p>
        {#if paid && items.length > 0}
            {#key items}
				{#each users as user}
					 {user.name}
					 {user.total}
				{/each}
				
		
            {/key}
        {:else}Waiting for items and paid.{/if}
    </p>
</main>
