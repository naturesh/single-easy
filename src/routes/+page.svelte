<script lang="ts">

    const dict : any = {
        lesson5: `The company implemented a new strategy to increase market share.
회사는 시장 점유율을 높이기 위해 새로운 전략을 실행했다.
Scientists are researching renewable energy sources to combat climate change.
과학자들은 기후 변화에 대응하기 위해 재생 가능한 에너지원을 연구하고 있다.
The museum curator carefully preserved the ancient artifacts.
박물관 큐레이터는 고대 유물들을 신중하게 보존했다.
Artificial intelligence is revolutionizing various industries.
인공지능은 다양한 산업을 혁신하고 있다.
The chef's signature dish combines traditional and modern culinary techniques.
그 셰프의 대표 요리는 전통적인 요리법과 현대적인 요리 기술을 결합했다.
The government implemented strict measures to control the spread of the virus.
정부는 바이러스의 확산을 통제하기 위해 엄격한 조치를 시행했다.
The new smartphone features advanced facial recognition technology.
새로운 스마트폰은 고급 안면 인식 기술을 탑재하고 있다.
The company's stock price surged after the announcement of a merger.
합병 발표 후 회사의 주가가 급등했다.
The architect designed the building to be both aesthetically pleasing and energy-efficient.
건축가는 건물을 미적으로 아름답고 에너지 효율적이도록 설계했다.
The diplomat skillfully negotiated a peace treaty between the two countries.
외교관은 두 나라 사이의 평화 조약을 능숙하게 협상했다.
`,
        lesson4: `The concert was postponed due to unforeseen circumstances.
예상치 못한 상황으로 인해 콘서트가 연기되었다.
She excelled in both academics and extracurricular activities.
그녀는 학업과 과외 활동 모두에서 뛰어난 성과를 보였다.
The company's innovative approach revolutionized the industry.
그 회사의 혁신적인 접근 방식이 업계를 혁명적으로 바꾸었다.
Environmental conservation is crucial for future generations.
환경 보존은 미래 세대를 위해 매우 중요하다.
The detective carefully examined the crime scene for clues.
형사는 단서를 찾기 위해 범죄 현장을 세심히 조사했다.
Regular exercise can significantly improve overall health.
규칙적인 운동은 전반적인 건강을 크게 향상시킬 수 있다.
The artist's latest exhibition showcases a unique blend of styles.
그 예술가의 최신 전시회는 독특한 스타일의 조화를 보여준다.
Effective communication is key to successful teamwork.
효과적인 의사소통은 성공적인 팀워크의 핵심이다.
The new policy aims to reduce carbon emissions by 30% within five years.
새로운 정책은 5년 내에 탄소 배출량을 30% 줄이는 것을 목표로 한다.
The ancient ruins provide valuable insights into past civilizations.
고대 유적은 과거 문명에 대한 귀중한 통찰력을 제공한다.
`,
        review: ``
    }

    var index : number = -1


    var selected : string = ''
    var dictionary : { ko : string, en : string }[] = []

    async function loadDict(x : string) {

        if(x == '' ) return

        dictionary = []
        const raw = (dict[x] as string).split('\n')


        for(let i=0; i<raw.length; i+=2) {
            dictionary.push({
                ko : raw[i+1],
                en : raw[i]
            })
        }

        console.debug('Load complete!!  data from ' + x)
        console.debug('Start session...')

        index = -1
        index = 0
    }

    

    var ko = ''
    var en : { d : string | undefined , b : boolean, e : boolean }[] = []

    async function processData(index : number) {

        if(index == -1) return
        else if (dictionary.length == 0) return

        const data = dictionary[index]
        
        ko = data.ko

        const rawen = data.en.split(' ')
       
        var created = []

        for(let i of rawen) {
            if(Math.random() > 1 - 0.9) {

                created.push({
                    d : i.at(0),
                    b : false,
                    e : false
                })
                created.push({
                    d : i.slice(1, i.length) ,
                    b : true,
                    e : true
                })

            }else {

                created.push({
                    d : i,
                    b : false,
                    e : true
                })

            }

            

        }

        en = created
       

    }

    $ : processData(index)

</script>





<div class="font-bold text-xl fixed top-7 left-7 h-fit">

    <div>
       easy.
       <span class="text-xs font-thin">
            <span class="ml-1 mr-1">[</span> 
            english
            <span class="ml-1 mr-1">]</span>
       </span>
       <div class="text-xs font-thin"> owner & developer : github-naturesh, 양태환 </div>
    </div>

    <div class="text-xs mt-5 flex gap-3 font-light">
        <button class="shadow-xl p-3 rounded-xl hover:scale-110 duration-200" on:click={ async () => loadDict('lesson4')}>L 4</button>
        <button class="shadow-xl p-3 rounded-xl hover:scale-110 duration-200" on:click={ async () => loadDict('lesson5')}>L 5</button>
        <button class="shadow-xl p-3 rounded-xl hover:scale-110 duration-200" on:click={ async () => loadDict('review')}>R E : {(dict.review.split('\n').length-1)/2}</button>
    </div>
    
</div>

<div class="flex flex-col justify-center items-center w-10/12">


    <!-- Question Area -->
    {#key index}
        <div class="font-mono text-lg leading-loose w-full">
            {#if en.length}
                {#each en as e}
                    <button class={e.b ? 'blur' : '' + 'inline-block duration-300 border-none'} on:click={ async () => { e.b = !e.b}}>
                        <span class={e.e ? 'mr-2' : ''}>
                            {e.d}
                        </span>
                    </button>
                {/each}
            {:else}
                Welcome to Easy. for english
            {/if}
            
        </div>
        <div class="font-mono text-sm leading-loose mt-16 shadow-sm rounded-xl p-3 w-full">
            { ko || '영단어 암기, 복습, 문장암기'}
        </div>
    {/key}

    <div class="mt-5 w-full fixed bottom-7">
        <div class="w-5/6 flex flex-row m-auto">
            <div class="w-1/4">
                <button class="h-14 w-5/6 m-auto block rounded-xl hover:scale-110 duration-200 bg-slate-50 text-slate-500 text-xs animate-bounce" on:click={ async () => index -= 1}>Back</button>
            </div>
            <div class="w-1/4">
                <button class="h-14 w-5/6 m-auto block rounded-xl hover:scale-110 duration-200 bg-slate-50 text-slate-500 text-xs animate-bounce" on:click={ async () => index += 1}>Next</button>
            </div>
            <div class="w-1/4">
                <button class="h-14 w-5/6 m-auto block rounded-xl hover:scale-110 duration-200 bg-slate-50 text-slate-500 text-xs animate-bounce" on:click={ async () => {
                    en = en.map( i => {
                        i.b = false
                        return i
                    })
                }}>show</button>
            </div>
            <div class="w-1/4">
                <button class="h-14 w-5/6 m-auto block rounded-xl hover:scale-110 duration-200 bg-slate-50 text-slate-500 text-xs" on:click={ async () =>{
                    const data = dictionary[index]

                    if(data) {
                        dict.review += data.en + '\n' + data.ko + '\n'
                        
                    }

                    index += 1

                }}>X</button>
            </div>
        </div>
    </div>
</div>


<style>
    :global(body) {
        touch-action: manipulation;
    }
</style>


