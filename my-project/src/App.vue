<template>
  <div class="grid grid-cols-1">
    <div
      v-if="fav"
      class="
        w-6/12
        absolute
        top-10
        right-0
        left-0
        z-50
        flex
        mx-auto
        p-4
        mb-4
        text-sm text-green-700
        bg-green-100
        rounded-lg
        dark:bg-green-200 dark:text-green-800
      "
      role="alert"
    >
      <!-- hhh  -->
      <svg
        aria-hidden="true"
        class="flex-shrink-0 inline w-5 h-5 mr-3"
        fill="currentColor"
        viewBox="0 0 20 20"
        xmlns="http://www.w3.org/2000/svg"
      >
        <path
          fill-rule="evenodd"
          d="M18 10a8 8 0 11-16 0 8 8 0 0116 0zm-7-4a1 1 0 11-2 0 1 1 0 012 0zM9 9a1 1 0 000 2v3a1 1 0 001 1h1a1 1 0 100-2v-3a1 1 0 00-1-1H9z"
          clip-rule="evenodd"
        ></path>
      </svg>
      <span class="sr-only">Info</span>
      <div>
        <span class="font-medium">{{ text }}</span>
      </div>
    </div>
    <div class="container mx-auto" style="min-height: 90vh">
      <div
        class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-4 gap-x-6 gap-y-10"
      >
        <div>
          <div>
            <h2 class="text-4xl mb-5 text-left font-extrabold dark:text-white">
              Catagories
            </h2>
          </div>
          <div
            v-for="items in info.drinks.slice(0, 10)"
            :key="items"
            class="
              w-48
              text-gray-900
              bg-white
              rounded-lg
              border border-gray-200
              dark:bg-gray-700 dark:border-gray-600 dark:text-white
            "
          >
            <button
              @click="searchByInd(items.strIngredient1)"
              type="button"
              class="
                inline-flex
                relative
                items-center
                py-2
                px-4
                w-full
                text-sm
                font-medium
                rounded-t-lg
                border-b border-gray-200
                hover:bg-gray-100 hover:text-blue-700
                focus:z-10 focus:ring-2 focus:ring-blue-700 focus:text-blue-700
                dark:border-gray-600
                dark:hover:bg-gray-600
                dark:hover:text-white
                dark:focus:ring-gray-500
                dark:focus:text-white
              "
            >
              <svg
                aria-hidden="true"
                class="mr-2 w-4 h-4 fill-current"
                fill="currentColor"
                viewBox="0 0 20 20"
                xmlns="http://www.w3.org/2000/svg"
              >
                <path
                  fill-rule="evenodd"
                  d="M18 10a8 8 0 11-16 0 8 8 0 0116 0zm-6-3a2 2 0 11-4 0 2 2 0 014 0zm-2 4a5 5 0 00-4.546 2.916A5.986 5.986 0 0010 16a5.986 5.986 0 004.546-2.084A5 5 0 0010 11z"
                  clip-rule="evenodd"
                ></path>
              </svg>
              {{ items.strIngredient1 }}
            </button>
          </div>
        </div>
        <div class="col-span-3">
          <h2
            v-if="coctails.drinks.length"
            class="text-4xl mb-5 text-left font-extrabold dark:text-white"
          >
            cocktails
          </h2>
          <div
            v-if="coctails.drinks.length"
            class="grid grid-cols-3 gap-4 mb-10"
          >
            <div
              v-for="cocktail in computedFav"
              :key="cocktail"
              class="relative"
            >
              <div
                class="
                  h-full
                  max-w-sm
                  bg-white
                  rounded-lg
                  border border-gray-200
                  shadow-md
                  dark:bg-gray-800 dark:border-gray-700
                "
              >
                <a href="#">
                  <img
                    class="rounded-t-lg"
                    :src="cocktail.strDrinkThumb"
                    alt=""
                  />
                </a>
                <div class="p-5">
                  <a href="#">
                    <h5
                      class="
                      h-16
                        mb-2
                        text-2xl
                        font-bold
                        tracking-tight
                        text-gray-900
                        dark:text-white
                      "
                    >
                      {{ cocktail.strDrink }}
                    </h5>
                  </a>

                  <button
                    @click="favAction(cocktail)"
                    type="button"
                    class="
                      w-10
                      absolute
                      top-0
                      right-0
                      left-0
                      z-50
                      text-white-400
                      bg-transparent
                      hover:bg-white-200 hover:text-white-900
                      rounded-lg
                      text-sm
                      p-1.5
                      ml-auto
                      inline-flex
                      items-center
                      dark:hover:bg-gray-600 dark:hover:text-white
                    "
                    data-modal-toggle="extralarge-modal"
                  >
                    <svg
                      v-if="cocktail.favr == -1"
                      xmlns="http://www.w3.org/2000/svg"
                      fill="none"
                      viewBox="0 0 24 24"
                      stroke-width="1.5"
                      stroke="currentColor"
                      class="w-6 h-6"
                    >
                      <path
                        stroke-linecap="round"
                        stroke-linejoin="round"
                        d="M21 8.25c0-2.485-2.099-4.5-4.688-4.5-1.935 0-3.597 1.126-4.312 2.733-.715-1.607-2.377-2.733-4.313-2.733C5.1 3.75 3 5.765 3 8.25c0 7.22 9 12 9 12s9-4.78 9-12z"
                      />
                    </svg>
                    <svg
                      v-else
                      xmlns="http://www.w3.org/2000/svg"
                      viewBox="0 0 24 24"
                      fill="red"
                      class="w-6 h-6"
                    >
                      <path
                        d="M11.645 20.91l-.007-.003-.022-.012a15.247 15.247 0 01-.383-.218 25.18 25.18 0 01-4.244-3.17C4.688 15.36 2.25 12.174 2.25 8.25 2.25 5.322 4.714 3 7.688 3A5.5 5.5 0 0112 5.052 5.5 5.5 0 0116.313 3c2.973 0 5.437 2.322 5.437 5.25 0 3.925-2.438 7.111-4.739 9.256a25.175 25.175 0 01-4.244 3.17 15.247 15.247 0 01-.383.219l-.022.012-.007.004-.003.001a.752.752 0 01-.704 0l-.003-.001z"
                      />
                    </svg>

                    <span class="sr-only">not fav hart</span>
                  </button>

                  <a
                    @click="DetailCocktail(cocktail.strDrink)"
                    href="#"
                    class="
                      inline-flex
                      items-center
                      py-2
                      px-3
                      text-sm
                      font-medium
                      text-center text-white
                      bg-blue-700
                      rounded-lg
                      hover:bg-blue-800
                      focus:ring-4 focus:outline-none focus:ring-blue-300
                      dark:bg-blue-600
                      dark:hover:bg-blue-700
                      dark:focus:ring-blue-800
                    "
                    data-modal-toggle="extralarge-modal"
                  >
                    Read more
                    <svg
                      aria-hidden="true"
                      class="ml-2 -mr-1 w-4 h-4"
                      fill="currentColor"
                      viewBox="0 0 20 20"
                      xmlns="http://www.w3.org/2000/svg"
                    >
                      <path
                        fill-rule="evenodd"
                        d="M10.293 3.293a1 1 0 011.414 0l6 6a1 1 0 010 1.414l-6 6a1 1 0 01-1.414-1.414L14.586 11H3a1 1 0 110-2h11.586l-4.293-4.293a1 1 0 010-1.414z"
                        clip-rule="evenodd"
                      ></path>
                    </svg>
                  </a>
                </div>
                <!-- model  -->
                <div
                  v-if="showFlie"
                  id="extralarge-modal"
                  tabindex="-1"
                  class="
                    overflow-y-auto overflow-x-hidden
                    fixed
                    top-50
                    right-0
                    left-0
                    z-50
                    w-full
                    md:inset-0
                    h-modal
                    md:h-full
                  "
                  :class="showFlie == false ? 'hidden' : 'visible'"
                >
                  <div
                    class="
                      mx-auto
                      relative
                      p-4
                      w-full
                      max-w-7xl
                      h-full
                      md:h-auto
                    "
                  >
                    <!-- Modal content -->
                    <div
                      class="
                        relative
                        bg-white
                        rounded-lg
                        shadow
                        dark:bg-gray-700
                      "
                    >
                      <!-- Modal header -->
                      <div
                        class="
                          flex
                          justify-between
                          items-center
                          p-5
                          rounded-t
                          border-b
                          dark:border-gray-600
                        "
                      >
                        <h3
                          class="
                            text-xl
                            font-medium
                            text-gray-900
                            dark:text-white
                          "
                        >
                          {{ detaledInfo.drinks[0].strDrink }}
                        </h3>
                        <button
                          @click="showFlie = false"
                          type="button"
                          class="
                            text-gray-400
                            bg-transparent
                            hover:bg-gray-200 hover:text-gray-900
                            rounded-lg
                            text-sm
                            p-1.5
                            ml-auto
                            inline-flex
                            items-center
                            dark:hover:bg-gray-600 dark:hover:text-white
                          "
                          data-modal-toggle="extralarge-modal"
                        >
                          <svg
                            aria-hidden="true"
                            class="w-5 h-5"
                            fill="currentColor"
                            viewBox="0 0 20 20"
                            xmlns="http://www.w3.org/2000/svg"
                          >
                            <path
                              fill-rule="evenodd"
                              d="M4.293 4.293a1 1 0 011.414 0L10 8.586l4.293-4.293a1 1 0 111.414 1.414L11.414 10l4.293 4.293a1 1 0 01-1.414 1.414L10 11.414l-4.293 4.293a1 1 0 01-1.414-1.414L8.586 10 4.293 5.707a1 1 0 010-1.414z"
                              clip-rule="evenodd"
                            ></path>
                          </svg>

                          <span class="sr-only">Close modal</span>
                        </button>
                      </div>
                      <!-- Modal body -->
                      <div
                        class="p-6 space-y-6"
                        v-for="info in detaledInfo.drinks"
                        :key="info"
                      >
                        <div class="grid grid-cols-4 gap-4">
                          <div class="...">
                            <img
                              class="rounded-t-lg aspect-square w-72 h-72"
                              :src="info.strDrinkThumb"
                              alt=""
                            />
                          </div>
                          <div class="col-span-3 ...">
                            <!-- <p
                          class="
                            text-base
                            leading-relaxed
                            text-gray-500
                            dark:text-gray-400
                          "
                        >
                          {{ info }}
                        </p> -->
                            <p
                              class="
                                text-left text-align-left
                                leading-relaxed
                                text-gray-500
                                dark:text-gray-400
                              "
                            >
                              <span class="font-bold">Drink Name : </span>
                              {{ info.strDrink }}
                            </p>
                            <p
                              class="
                                text-left text-align-left
                                leading-relaxed
                                text-gray-500
                                dark:text-gray-400
                              "
                            >
                              <span class="font-bold">Drink Category : </span>
                              {{ info.strAlcoholic }}
                            </p>
                            <p
                              class="
                                text-left text-align-left
                                leading-relaxed
                                text-gray-500
                                dark:text-gray-400
                              "
                            >
                              <span class="font-bold">Serveing Glass : </span>
                              {{ info.strGlass }}
                            </p>
                            <p
                              class="
                                text-left text-align-left
                                leading-relaxed
                                text-gray-500
                                dark:text-gray-400
                              "
                            >
                              <span class="font-bold">Ingredient : </span>
                              <span v-if="info.strIngredient1"
                                >({{ info.strMeasure1 }})
                                {{ info.strIngredient1 }}</span
                              ><span v-if="info.strIngredient2"
                                >, ({{ info.strMeasure2 }})
                                {{ info.strIngredient2 }}</span
                              ><span v-if="info.strIngredient3"
                                >, ({{ info.strMeasure3 }})
                                {{ info.strIngredient3 }}</span
                              ><span v-if="info.strIngredient4"
                                >, ({{ info.strMeasure4 }})
                                {{ info.strIngredient4 }}</span
                              ><span v-if="info.strIngredient5"
                                >, ({{ info.strMeasure5 }})
                                {{ info.strIngredient5 }}</span
                              ><span v-if="info.strIngredient6"
                                >, ({{ info.strMeasure6 }})
                                {{ info.strIngredient6 }}</span
                              ><span v-if="info.strIngredient7"
                                >, ({{ info.strMeasure7 }})
                                {{ info.strIngredient7 }}</span
                              ><span v-if="info.strIngredient8"
                                >, ({{ info.strMeasure8 }})
                                {{ info.strIngredient8 }}</span
                              ><span v-if="info.strIngredient9"
                                >, ({{ info.strMeasure9 }})
                                {{ info.strIngredient9 }}</span
                              ><span v-if="info.strIngredient10"
                                >, ({{ info.strMeasure10 }})
                                {{ info.strIngredient10 }}</span
                              ><span v-if="info.strIngredient11"
                                >, ({{ info.strMeasure11 }})
                                {{ info.strIngredient11 }}</span
                              ><span v-if="info.strIngredient12"
                                >, ({{ info.strMeasure12 }})
                                {{ info.strIngredient12 }}</span
                              ><span v-if="info.strIngredient13"
                                >, ({{ info.strMeasure13 }})
                                {{ info.strIngredient13 }}</span
                              >
                              <span v-if="info.strIngredient14"
                                >, ({{ info.strMeasure14 }})
                                {{ info.strIngredient14 }}</span
                              >
                            </p>
                            <p
                              class="
                                text-left text-align-left
                                leading-relaxed
                                text-gray-500
                                dark:text-gray-400
                              "
                            >
                              <span class="font-bold">Description : </span>
                              {{ info.strInstructions }}
                            </p>
                          </div>
                        </div>
                      </div>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <h2 class="text-4xl mb-5 text-left font-extrabold dark:text-white">
            Favourties cocktails
          </h2>
          <div v-if="local" class="grid grid-cols-3 gap-4">
            <div v-for="cocktail in local" :key="cocktail" class="relative">
              <div
                class="
                  h-full
                  max-w-sm
                  bg-white
                  rounded-lg
                  border border-gray-200
                  shadow-md
                  dark:bg-gray-800 dark:border-gray-700
                "
              >
                <a href="#">
                  <img
                    class="rounded-t-lg"
                    :src="cocktail.favcocktail.strDrinkThumb"
                    alt=""
                  />
                </a>
                <div class="p-5">
                  <a href="#">
                    <h5
                      class="
                      h-16
                        mb-2
                        text-2xl
                        font-bold
                        tracking-tight
                        text-gray-900
                        dark:text-white
                      "
                    >
                      {{ cocktail.favcocktail.strDrink }}
                    </h5>
                  </a>

                  <button
                    type="button"
                    class="
                      w-10
                      absolute
                      top-0
                      right-0
                      left-0
                      z-50
                      text-white-400
                      bg-transparent
                      hover:bg-white-200 hover:text-white-900
                      rounded-lg
                      text-sm
                      p-1.5
                      ml-auto
                      inline-flex
                      items-center
                      dark:hover:bg-gray-600 dark:hover:text-white
                    "
                    data-modal-toggle="extralarge-modal"
                  >
                    <svg
                      v-if="cocktail.favr == -1"
                      xmlns="http://www.w3.org/2000/svg"
                      fill="none"
                      viewBox="0 0 24 24"
                      stroke-width="1.5"
                      stroke="currentColor"
                      class="w-6 h-6"
                    >
                      <path
                        stroke-linecap="round"
                        stroke-linejoin="round"
                        d="M21 8.25c0-2.485-2.099-4.5-4.688-4.5-1.935 0-3.597 1.126-4.312 2.733-.715-1.607-2.377-2.733-4.313-2.733C5.1 3.75 3 5.765 3 8.25c0 7.22 9 12 9 12s9-4.78 9-12z"
                      />
                    </svg>
                    <svg
                      v-else
                      xmlns="http://www.w3.org/2000/svg"
                      viewBox="0 0 24 24"
                      fill="red"
                      class="w-6 h-6"
                    >
                      <path
                        d="M11.645 20.91l-.007-.003-.022-.012a15.247 15.247 0 01-.383-.218 25.18 25.18 0 01-4.244-3.17C4.688 15.36 2.25 12.174 2.25 8.25 2.25 5.322 4.714 3 7.688 3A5.5 5.5 0 0112 5.052 5.5 5.5 0 0116.313 3c2.973 0 5.437 2.322 5.437 5.25 0 3.925-2.438 7.111-4.739 9.256a25.175 25.175 0 01-4.244 3.17 15.247 15.247 0 01-.383.219l-.022.012-.007.004-.003.001a.752.752 0 01-.704 0l-.003-.001z"
                      />
                    </svg>

                    <span class="sr-only">not fav hart</span>
                  </button>

                  <a
                    @click="DetailCocktail(cocktail.favcocktail.strDrink)"
                    href="#"
                    class="
                      inline-flex
                      items-center
                      py-2
                      px-3
                      text-sm
                      font-medium
                      text-center text-white
                      bg-blue-700
                      rounded-lg
                      hover:bg-blue-800
                      focus:ring-4 focus:outline-none focus:ring-blue-300
                      dark:bg-blue-600
                      dark:hover:bg-blue-700
                      dark:focus:ring-blue-800
                    "
                    data-modal-toggle="extralarge-modal"
                  >
                    Read more
                    <svg
                      aria-hidden="true"
                      class="ml-2 -mr-1 w-4 h-4"
                      fill="currentColor"
                      viewBox="0 0 20 20"
                      xmlns="http://www.w3.org/2000/svg"
                    >
                      <path
                        fill-rule="evenodd"
                        d="M10.293 3.293a1 1 0 011.414 0l6 6a1 1 0 010 1.414l-6 6a1 1 0 01-1.414-1.414L14.586 11H3a1 1 0 110-2h11.586l-4.293-4.293a1 1 0 010-1.414z"
                        clip-rule="evenodd"
                      ></path>
                    </svg>
                  </a>
                </div>
                <!-- model  -->
                <div
                  v-if="showFlie"
                  id="extralarge-modal"
                  tabindex="-1"
                  class="
                    overflow-y-auto overflow-x-hidden
                    fixed
                    top-50
                    right-0
                    left-0
                    z-50
                    w-full
                    md:inset-0
                    h-modal
                    md:h-full
                  "
                  :class="showFlie == false ? 'hidden' : 'visible'"
                >
                  <div
                    class="
                      mx-auto
                      relative
                      p-4
                      w-full
                      max-w-7xl
                      h-full
                      md:h-auto
                    "
                  >
                    <!-- Modal content -->
                    <div
                      class="
                        relative
                        bg-white
                        rounded-lg
                        shadow
                        dark:bg-gray-700
                      "
                    >
                      <!-- Modal header -->
                      <div
                        class="
                          flex
                          justify-between
                          items-center
                          p-5
                          rounded-t
                          border-b
                          dark:border-gray-600
                        "
                      >
                        <h3
                          class="
                            text-xl
                            font-medium
                            text-gray-900
                            dark:text-white
                          "
                        >
                          {{ detaledInfo.drinks[0].strDrink }}
                        </h3>
                        <button
                          @click="showFlie = false"
                          type="button"
                          class="
                            text-gray-400
                            bg-transparent
                            hover:bg-gray-200 hover:text-gray-900
                            rounded-lg
                            text-sm
                            p-1.5
                            ml-auto
                            inline-flex
                            items-center
                            dark:hover:bg-gray-600 dark:hover:text-white
                          "
                          data-modal-toggle="extralarge-modal"
                        >
                          <svg
                            aria-hidden="true"
                            class="w-5 h-5"
                            fill="currentColor"
                            viewBox="0 0 20 20"
                            xmlns="http://www.w3.org/2000/svg"
                          >
                            <path
                              fill-rule="evenodd"
                              d="M4.293 4.293a1 1 0 011.414 0L10 8.586l4.293-4.293a1 1 0 111.414 1.414L11.414 10l4.293 4.293a1 1 0 01-1.414 1.414L10 11.414l-4.293 4.293a1 1 0 01-1.414-1.414L8.586 10 4.293 5.707a1 1 0 010-1.414z"
                              clip-rule="evenodd"
                            ></path>
                          </svg>

                          <span class="sr-only">Close modal</span>
                        </button>
                      </div>
                      <!-- Modal body -->
                      <div
                        class="p-6 space-y-6"
                        v-for="info in detaledInfo.drinks"
                        :key="info"
                      >
                        <div class="grid grid-cols-4 gap-4">
                          <div class="...">
                            <img
                              class="rounded-t-lg aspect-square w-72 h-72"
                              :src="info.strDrinkThumb"
                              alt=""
                            />
                          </div>
                          <div class="col-span-3 ...">
                            <!-- <p
                          class="
                            text-base
                            leading-relaxed
                            text-gray-500
                            dark:text-gray-400
                          "
                        >
                          {{ info }}
                        </p> -->
                            <p
                              class="
                                text-left text-align-left
                                leading-relaxed
                                text-gray-500
                                dark:text-gray-400
                              "
                            >
                              <span class="font-bold">Drink Name : </span>
                              {{ info.strDrink }}
                            </p>
                            <p
                              class="
                                text-left text-align-left
                                leading-relaxed
                                text-gray-500
                                dark:text-gray-400
                              "
                            >
                              <span class="font-bold">Drink Category : </span>
                              {{ info.strAlcoholic }}
                            </p>
                            <p
                              class="
                                text-left text-align-left
                                leading-relaxed
                                text-gray-500
                                dark:text-gray-400
                              "
                            >
                              <span class="font-bold">Serveing Glass : </span>
                              {{ info.strGlass }}
                            </p>
                            <p
                              class="
                                text-left text-align-left
                                leading-relaxed
                                text-gray-500
                                dark:text-gray-400
                              "
                            >
                              <span class="font-bold">Ingredient : </span>
                              <span v-if="info.strIngredient1"
                                >({{ info.strMeasure1 }})
                                {{ info.strIngredient1 }}</span
                              ><span v-if="info.strIngredient2"
                                >, ({{ info.strMeasure2 }})
                                {{ info.strIngredient2 }}</span
                              ><span v-if="info.strIngredient3"
                                >, ({{ info.strMeasure3 }})
                                {{ info.strIngredient3 }}</span
                              ><span v-if="info.strIngredient4"
                                >, ({{ info.strMeasure4 }})
                                {{ info.strIngredient4 }}</span
                              ><span v-if="info.strIngredient5"
                                >, ({{ info.strMeasure5 }})
                                {{ info.strIngredient5 }}</span
                              ><span v-if="info.strIngredient6"
                                >, ({{ info.strMeasure6 }})
                                {{ info.strIngredient6 }}</span
                              ><span v-if="info.strIngredient7"
                                >, ({{ info.strMeasure7 }})
                                {{ info.strIngredient7 }}</span
                              ><span v-if="info.strIngredient8"
                                >, ({{ info.strMeasure8 }})
                                {{ info.strIngredient8 }}</span
                              ><span v-if="info.strIngredient9"
                                >, ({{ info.strMeasure9 }})
                                {{ info.strIngredient9 }}</span
                              ><span v-if="info.strIngredient10"
                                >, ({{ info.strMeasure10 }})
                                {{ info.strIngredient10 }}</span
                              ><span v-if="info.strIngredient11"
                                >, ({{ info.strMeasure11 }})
                                {{ info.strIngredient11 }}</span
                              ><span v-if="info.strIngredient12"
                                >, ({{ info.strMeasure12 }})
                                {{ info.strIngredient12 }}</span
                              ><span v-if="info.strIngredient13"
                                >, ({{ info.strMeasure13 }})
                                {{ info.strIngredient13 }}</span
                              >
                              <span v-if="info.strIngredient14"
                                >, ({{ info.strMeasure14 }})
                                {{ info.strIngredient14 }}</span
                              >
                            </p>
                            <p
                              class="
                                text-left text-align-left
                                leading-relaxed
                                text-gray-500
                                dark:text-gray-400
                              "
                            >
                              <span class="font-bold">Description : </span>
                              {{ info.strInstructions }}
                            </p>
                          </div>
                        </div>
                      </div>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div v-else>
            <div
              class="
                p-4
                mb-4
                text-sm text-green-700
                bg-green-100
                rounded-lg
                dark:bg-green-200 dark:text-green-800
              "
              role="alert"
            >
              <span class="font-medium">No Favourties are added, Please click on the catagories to search cocktails.</span>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- <HelloWorld msg="Vite + Vue" /> -->
  </div>
</template>

<script>
import axios from "axios";
// import HelloWorld from "./components/HelloWorld.vue";
export default {
  name: "App",
  components: {
    // HelloWorld,
  },
  data() {
    return {
      clickedCat: "",
      local: [],
      text: "",
      fav: false,
      showFlie: false,
      info: "",
      coctails: {
        drinks: [],
      },
      detaledInfo: "",
    };
  },
  created() {
    this.local = JSON.parse(localStorage.getItem("favItems"));
    // getList() {

    axios
      .get("https://www.thecocktaildb.com/api/json/v1/1/list.php?i=list")
      .then((response) => {
        this.info = response.data;
      });
    // },
  },
  methods: {
    favAction(details) {
      var localstorageData = JSON.parse(localStorage.getItem("favItems"));

      // when there are no fav
      if (localstorageData == null) {
        var drink = [];
        drink.push({
          idDrink: details.idDrink,
          favcocktail: details,
        });
        localStorage.setItem("favItems", JSON.stringify(drink));
        // return;
      } else {
        let index = localstorageData.findIndex(
          (el) => el.idDrink == details.idDrink
        );
        if (index == -1) {
          localstorageData.push({
            idDrink: details.idDrink,
            favcocktail: details,
          });

          localStorage.setItem("favItems", JSON.stringify(localstorageData));
          this.fav = true;
          this.text = details.strDrink + " _" + " is added to faviroutes";
          // return;
        } else {
          localstorageData = localstorageData.filter(
            (el) => el.idDrink != details.idDrink
          );
          localStorage.setItem("favItems", JSON.stringify(localstorageData));
          this.fav = true;
          this.text = details.strDrink + " _" + " is deleted from faviroutes";
        }
      }
      this.local = JSON.parse(localStorage.getItem("favItems"));

      setTimeout(() => {
        this.fav = false;
      }, 4000);
    },
    isfav(drinkid) {
      if (this.local == null) {
        return false;
      }

      let index = this.local.findIndex((el) => el.idDrink == drinkid);
      return index != -1;
    },
    DetailCocktail(drink) {
      this.showFlie = true;
      axios
        .get(
          `https://www.thecocktaildb.com/api/json/v1/1/search.php?s=${drink}`
        )
        .then((response) => {
          console.log(response);
          this.detaledInfo = response.data;
        });
    },
    searchByInd(item) {
      // alert(90);
      this.clickedCat = item;
      axios
        .get(`https://www.thecocktaildb.com/api/json/v1/1/filter.php?i=${item}`)
        .then((response) => {
          this.coctails = response.data;
        });
    },
  },
  computed: {
    computedFav() {
      // if (this.local == null) {
      //   return this.coctails.drinks;
      // }

      this.coctails.drinks.forEach((element) => {
        if (this.local == null) {
          element.favr = -1;
        } else {
          element.favr = this.local.findIndex(
            (el) => element.idDrink == el.idDrink
          );
        }
      });
      return this.coctails.drinks;
      //  let index = this.local.findIndex(
      //     (el) => el.idDrink == drinkid
      //   );
      //   return index != -1
    },
  },
  // created() {
  //   this.axios
  //     .get("www.thecocktaildb.com/api/json/v1/1/list.php?i=list")
  //     .then((response) => {
  //       this.info = response;
  //     });

  // },
};
</script>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>








