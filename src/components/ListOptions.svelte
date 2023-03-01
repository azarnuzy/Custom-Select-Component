<script>
  import { each } from 'svelte/internal';

  let options = [
    {
      category: 'Beef',
      foods: [
        { id: '1A', value: 'Beef and Mustard Pie', isSelected: false },
        { id: '2A', value: 'Beef and Oyster Pie', isSelected: false },
        { id: '3A', value: 'Beef Bourguignon', isSelected: false },
        { id: '4A', value: 'Beef Brisket Pot Roast', isSelected: false },
      ],
    },
    {
      category: 'Chicken',
      foods: [
        { id: '1B', value: 'Ayam Percik', isSelected: false },
        { id: '2B', value: 'Brown Stew Chicken', isSelected: false },
        { id: '3B', value: 'Chick-Fil-A Sandwich', isSelected: false },
        { id: '4B', value: 'Chicken & Mushroom Hotpot', isSelected: false },
        { id: '5B', value: 'Chicken Alfredo Primavera', isSelected: false },
      ],
    },
    {
      category: 'Dessert',
      foods: [
        { id: '1C', value: 'Apam Balik', isSelected: false },
        { id: '2C', value: 'Apple & Blackberry Crumble', isSelected: false },
        { id: '3C', value: 'Apple Frangipan Tart', isSelected: false },
        { id: '4C', value: 'Bakewell Tart', isSelected: false },
        { id: '5C', value: 'Banana Pancakes', isSelected: false },
      ],
    },
    {
      category: 'Seafood',
      foods: [
        {
          id: '1D',
          value: 'Baked Salmon with Fennel & Tomatoes',
          isSelected: false,
        },
        { id: '2D', value: 'Cajun Spiced Fish Tacos', isSelected: false },
        { id: '3D', value: 'Escovitch Fish', isSelected: false },
        { id: '4D', value: 'Fish Fofos', isSelected: false },
      ],
    },
  ];

  let query = '';
  let filteredOptions = options;
  let selected = [];

  let isFocus = false;

  const handleFocus = () => {
    isFocus = true;
  };

  const handleBlur = () => (isFocus = false);

  const handleChange = (e) => {
    query = e.target.value;
    const tempFilteredOptions = options.reduce((acc, option) => {
      if (option.category.toLowerCase().includes(query.toLowerCase())) {
        return [...acc, option];
      }

      const filteredFoods = option.foods.filter((food) =>
        food.value.toLowerCase().includes(query.toLowerCase())
      );
      if (filteredFoods.length > 0) {
        return [...acc, { ...option, foods: filteredFoods }];
      }
      return acc;
    }, []);

    filteredOptions = [...tempFilteredOptions];
  };

  const handleClick = (props) => {
    options.forEach((option) =>
      option.foods.forEach((food) => {
        if (food.id === props.id) {
          food.isSelected = !props.isSelected;
        }
      })
    );

    filteredOptions = [...options];
    const selectedOptions = options.reduce((acc, curr) => {
      const selectedFoods = curr.foods.filter((food) => food.isSelected);
      if (selectedFoods.length > 0) {
        acc.push({
          category: curr.category,
          foods: selectedFoods,
        });
      }
      return acc;
    }, []);

    selected = [...selectedOptions];
  };
</script>

<div class="container">
  <div class="wrapper-selected">
    <ul class="selected-options">
      {#each selected as food (food.category)}
        {#each food.foods as select}
          <li>{select.value}</li>
        {/each}
      {/each}
    </ul>
  </div>
  <div class="list">
    <div class="list-input">
      <input
        on:focus={handleFocus}
        on:input={(e) => handleChange(e)}
        value={query}
        type="text"
        placeholder="Search Your Favorite Foods"
      />
      <button
        class={isFocus ? ' show x-icon' : ' hidden'}
        on:click={handleBlur}
      >
        <svg
          width="31"
          height="17"
          viewBox="0 0 31 17"
          fill="none"
          xmlns="http://www.w3.org/2000/svg"
        >
          <path
            d="M11.625 4.95837L14.2083 8.50004L11.625 12.0417H14.2083L15.5 10.2709L16.7917 12.0417H19.375L16.7917 8.50004L19.375 4.95837H16.7917L15.5 6.72921L14.2083 4.95837H11.625Z"
            fill="currentColor"
          />
        </svg>
      </button>
    </div>
    <div class="list-options {isFocus ? ' show' : ' hidden'}">
      {#each filteredOptions as option (option.category)}
        <h3>{option.category}</h3>
        <ul>
          {#each option.foods as food (food.id)}
            <li
              class="{food.isSelected === true ? ' active-list' : ''} list-food"
            >
              <button on:click={() => handleClick(food)}>
                {food.value}
                <span
                  class="{food.isSelected ? ' show' : ' hidden'} icon-checklist"
                >
                  <svg
                    width="24"
                    height="24"
                    viewBox="0 0 24 24"
                    fill="none"
                    xmlns="http://www.w3.org/2000/svg"
                  >
                    <path
                      d="M10 16.4L6 12.4L7.4 11L10 13.6L16.6 7L18 8.4L10 16.4Z"
                      fill="#F8F8F8"
                    />
                  </svg>
                </span>
              </button>
            </li>
          {/each}
        </ul>
      {:else}
        <h3>There is no result '{query}'</h3>
      {/each}
    </div>
  </div>
</div>

<style>
  button {
    padding: 0;
    margin: 0;
    background-color: transparent;
    border: transparent;
    cursor: pointer;
  }

  .container {
    display: flex;
    width: 720px;
    justify-content: center;
    flex-direction: column;
    align-items: center;
  }

  .wrapper-selected {
    height: 50px;
    width: 83%;
  }

  .selected-options {
    display: flex;
    gap: 12px;
    overflow-x: scroll;
    list-style: none;
    padding: 0;
    max-width: 100%;
  }

  .selected-options li {
    text-align: center;
    list-style: none;
    min-width: fit-content;
    padding: 4px 8px;
    color: #fff;
    border-radius: 10px;
    font-weight: 600;
    background-color: #14b8a6;
    margin-bottom: 5px;
  }

  .list {
    width: 100%;
    display: flex;
    position: relative;
    flex-direction: column;
    align-items: center;
  }

  .show {
    display: block;
  }

  .hidden {
    display: none;
  }

  .x-icon {
    cursor: pointer;
  }

  ::-webkit-scrollbar-track {
    -webkit-box-shadow: inset 0 0 6px rgba(0, 0, 0, 0.3);
    background-color: #f5f5f5;
  }

  ::-webkit-scrollbar {
    height: 5px;
    width: 5px;
    background-color: #0d9488;
  }

  ::-webkit-scrollbar-thumb {
    background-color: #0d9488;
    border: 2px solid #0d9488;
  }

  .list-input {
    width: 80%;
    margin-top: 20px;
    background-color: #ffffff;
    border-radius: 30px;
    padding: 5px 10px;
    display: flex;
    align-items: center;
  }

  .list-input input {
    width: 100%;
    margin: 0;
    border: none;
  }

  input:focus {
    outline: none;
  }

  ul {
    list-style: none;
    padding: 0;
    margin: 0;
  }

  .list-options {
    background-color: #fff;
    border-radius: 5px;
    margin-top: 6px;
    width: 83%;
    position: absolute;
    top: 60px;
    max-height: 300px;
    overflow-y: scroll;
  }

  .list-options h3 {
    margin: 0;
    border-bottom: #dbdbdb 1px solid;
    padding: 5px;
    background-color: #0d9488;
    color: white;
  }

  .list-options ul li {
    margin: 0;
    display: flex;
    align-items: center;
    border-bottom: #dbdbdb 1px solid;
    cursor: pointer;
  }

  .list-options button {
    width: 100%;
    padding: 5px 20px;
    text-align: left;
  }

  .list-options ul li:hover,
  .list-options button:hover {
    background-color: #14b8a6;
    color: white;
  }

  .active-list button {
    background-color: #14b8a6;
    color: white;
  }

  .list-food button {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  .icon-checklist {
    display: flex;
    align-items: center;
  }
</style>
