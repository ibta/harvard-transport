<script lang="ts">
    import {Autocomplete, TabGroup, Tab, popup} from '@skeletonlabs/skeleton';
    import type {AutocompleteOption} from '@skeletonlabs/skeleton';
    import type {PopupSettings} from '@skeletonlabs/skeleton';

    let tabSet: number = 0;

    const departList: AutocompleteOption[] = [
        {
            label: '1 Western Ave',
            value: 'oneWestern',
            keywords: 'one, western, ave, one western, allston'
        },
        {
            label: "Barry's Corner (to square)",
            value: 'barrysCornerToSquare',
            keywords: 'one, western, ave, one western, allston'
        },
        {
            label: "Barry's Corner (to SEC)",
            value: 'barrysCornerToSEC',
            keywords: 'one, western, ave, one western, allston'
        },
        {
            label: 'Cambridge Common',
            value: 'cambridgeCommon',
            keywords: 'cambridge, common, cambridge common'
        },
        {label: 'Harvard Square (to mem hall)', value: 'HarvardSquareScienceCenter', keywords: 'sci center, mem hall, science center, memorial hall'},
        {label: 'Harvard Square (Southbound)', value: 'HarvardSquareScienceCenter', keywords: ''},
        {label: 'Kennedy School (Northbound)', value: '', keywords: ''},
        {label: 'Kennedy School (Southbound)', value: '', keywords: ''},
        {label: 'Lamont Library', value: '', keywords: ''},
        {
            label: 'Law School',
            value: 'lawSchool',
            keywords: 'harvard, law, school, hemenway',
            meta: {servicedBy: ['bus3']}
        },
        {label: 'Leverett', value: '', keywords: ''},
        {
            label: 'Mass & Garden',
            value: 'massgarden',
            keywords: 'mass, garden, mass and garden, mass & garden'
        },
        {label: 'Mather', value: '', keywords: ''},
        {label: 'Maxwell Dworkin', value: '', keywords: ''},
        {label: 'Memorial Hall', value: '', keywords: ''},
        {label: 'Quad', value: 'quad', keywords: 'quad, radcliffe, quadrangle'},
        {
            label: 'Radcliffe Yard',
            value: 'radcliffe',
            keywords: 'radcliffe yard, radcliffe, institute'
        },
        {label: 'Science Center', value: '', keywords: ''},
        {label: 'SEC', value: '', keywords: ''},
        {label: 'Harvard Stadium (Northbound)', value: '', keywords: ''},
        {label: 'Harvard Stadium (Southbound)', value: '', keywords: ''},
        {label: 'The Inn', value: '', keywords: ''},
        {label: 'Widener Gate', value: '', keywords: ''},
        {label: 'Winthrop', value: '', keywords: '', meta: {servicedBy: ['bus1', 'bus2']}}
    ];

    const destList: AutocompleteOption[] = [
        {label: 'Quad', value: 'quad', keywords: 'quad, radcliffe, quadrangle'}
    ];

    let popupDepart: PopupSettings = {
        event: 'focus-click',
        target: 'popupAutocompleteDepart',
        placement: 'bottom'
    };

    let popupDest: PopupSettings = {
        event: 'focus-click',
        target: 'popupAutocompleteDest',
        placement: 'bottom'
    };

    // console.log(departList.slice(3));

    let departFrom = '';
    let arriveAt = '';

    // let inputPopupDemo: string = "";

    function onDepartSelect(event: CustomEvent<AutocompleteOption>): void {
        departFrom = event.detail.label;
    }

    function onDestSelection(event: CustomEvent<AutocompleteOption>): void {
        arriveAt = event.detail.label;
    }
</script>

<!--  -->
<main class="container mx-auto p-6">
    <div class="flex flex-row justify-center items-center pb-8">
        <h2 class="h2 font-bold">get to dest</h2>
    </div>
    <div class="flex flex-row justify-center items-center lg:gap-24 md:gap-24 gap-6">
        <div class="lg:w-1/4 w-full">
            <label for="#departFrom" class="font-bold text-lg pb-2">
                from:
            </label>
            <input
                    class="input autocomplete"
                    type="search"
                    name="autocomplete-search"
                    bind:value={departFrom}
                    placeholder="mather!mather!mather!"
                    use:popup={popupDepart}
                    id="departFrom"
            />
            <div
                    data-popup="popupAutocompleteDepart"
                    class="card w-full max-w-sm max-h-48 p-4 overflow-y-auto"
                    tabindex="-1"
            >
                <Autocomplete bind:input={departFrom} options={departList} on:selection={onDepartSelect}/>
            </div>
        </div>

        <div class="lg:w-1/4 w-full">
            <label for="#arriveAt" class="font-bold h3 pb-2">
                to:
            </label>
            <input
                    class="input autocomplete"
                    type="search"
                    name="autocomplete-search"
                    bind:value={arriveAt}
                    placeholder="quad!quad!quad!"
                    use:popup={popupDest}
                    id="#arriveAt"
            />
            <div
                    data-popup="popupAutocompleteDest"
                    class="card w-full max-w-sm max-h-48 p-4 overflow-y-auto"
                    tabindex="-1"
            >
                <Autocomplete bind:input={arriveAt} options={destList} on:selection={onDestSelection}/>
            </div>
        </div>
    </div>
    <div class="pt-16">
        <h3 class="h4 font-bold">
            Buses available at stop:
        </h3>
        <div class="justify-center items-center pt-8 w-full">
            <div class="table-container row-start-2">
                <table class="table table-hover">
                    <thead>
                    <tr>
                        <!--{#if departFrom !== "" && departList.some(location => location.label.toLowerCase() === departFrom.toLowerCase())}-->
                        <!--	<th>DEPARTING {departFrom.toUpperCase()} AT:</th>-->
                        <!--{:else}-->
                        <!--	<th>DEPARTING ... AT:</th>-->
                        <!--{/if}-->

                        <!--{#if arriveAt !== "" && destList.some(location => location.label.toLowerCase() === arriveAt.toLowerCase())}-->
                        <!--	<th>ARRIVING AT {arriveAt.toUpperCase()}: </th>-->
                        <!--{:else}-->
                        <!--	<th>ARRIVING AT ...:</th>-->
                        <!--{/if}-->

                        <!-- make this conditional -->

                        <th>bus 1</th>
                        <th>bus 2</th>
                        <th>bus 3</th>
                        <th>bus 4</th>
                        <th>bus 5</th>

                        <th></th>
                    </tr>
                    </thead>
                    <tbody>
                    <tr>
                        <td>{departFrom}</td>
                        <td>{arriveAt}</td>
                    </tr>
                    </tbody>
                </table>
            </div>

        </div>
        <div class="justify-center items-center pt-32">
            <div class="table-container row-start-2">
                <table class="table table-hover">
                    <thead>
                    <tr>
                        {#if departFrom !== "" && departList.some(location => location.label.toLowerCase() === departFrom.toLowerCase())}
                            <th>DEPARTING {departFrom.toUpperCase()} AT:</th>
                        {:else}
                            <th>DEPARTING ... AT:</th>
                        {/if}

                        {#if arriveAt !== "" && destList.some(location => location.label.toLowerCase() === arriveAt.toLowerCase())}
                            <th>ARRIVING AT {arriveAt.toUpperCase()}:</th>
                        {:else}
                            <th>ARRIVING AT ...:</th>
                        {/if}

                        <th></th>
                    </tr>
                    </thead>
                    <tbody>
                    <tr>
                        <td>{departFrom}</td>
                        <td>{arriveAt}</td>
                    </tr>
                    </tbody>
                </table>
            </div>

            <!-- <TabGroup>
                <Tab bind:group={tabSet} name="tab1" value={0}>
                    <svelte:fragment slot="lead">(icon)</svelte:fragment>
                    <span>(available shuttle one)</span>
                </Tab>
                <Tab bind:group={tabSet} name="tab2" value={1}>(label 2)</Tab>
                <Tab bind:group={tabSet} name="tab3" value={2}>(label 3)</Tab>
                <svelte:fragment slot="panel">
                    {#if tabSet === 0}
                        (tab panel 1 contents)
                    {:else if tabSet === 1}
                        (tab panel 2 contents)
                    {:else if tabSet === 2}
                        (tab panel 3 contents)
                    {/if}
                </svelte:fragment>
            </TabGroup> -->

            <!-- <div class="table-container">
                <table class="table table-hover">
                    <thead>
                        <tr>

                        </tr>
                    </thead>
                </table> -->
        </div>
    </div>
</main>
