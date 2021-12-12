<template>
  <div class="min-h-screen overflow-hidden bg-white">
    <div class="flex min-h-screen overflow-x-auto" style="scroll-snap-type: x mandatory;">
    
      <div :class="['w-screen min-h-screen']" style="scroll-snap-align: start;scroll-snap-stop: always;" >
        <div class="w-screen min-h-screen flex justify-center items-center">
          
            <div class="m-2 text-2xl font-bold">
            　消防設備士乙種6類
            </div>
        </div>
      </div>

      <div :class="['w-screen min-h-screen']" style="scroll-snap-align: start;scroll-snap-stop: always;" v-for="(test, test_idx) in tests ">

        <div class="w-screen min-h-screen flex justify-center items-center">
          <div>
            <div class="m-2 text-2xl font-bold">
            {{ test.question}}
            </div>
            <div class="p-4 flex justify-center items-center">
              <RadioGroup v-model="test.selected">
                <div class="space-y-4">
                  <RadioGroupOption as="template" v-for="(choice, choice_idx) in test.choices" :key="choice.choice" :value="choice" v-slot="{ checked, active }">
                    <div v-on:click="answer_select(test,choice)" :class="[checked ? 'border-transparent' : 'border-gray-300', active ? 'ring-2 ring-indigo-500' : '', 'relative block bg-white border rounded-lg shadow-sm px-6 py-4 cursor-pointer sm:flex sm:justify-between focus:outline-none']">
                      <div class="flex items-center">
                        <div class="text-sm">
                          <RadioGroupLabel as="p" class="font-medium text-gray-900 ">
                            {{ choice.choice }}
                          </RadioGroupLabel>
                        </div>
                      </div>
                      <div :class="[active ? 'border' : 'border-2', checked ? 'border-indigo-500' : 'border-transparent', 'absolute -inset-px rounded-lg pointer-events-none']" aria-hidden="true" />
                    </div>
                  </RadioGroupOption>
                </div>
              </RadioGroup>
            </div>
            <div class="p-4 flex justify-center items-center">
            　{{ test_idx + 1 }} / {{ tests.length }}
            </div>
          </div>
        </div>


        <div v-if="test.correct_answer_flg" class="absolute top-0 left-0 w-screen min-h-screen flex justify-center items-center">
          <div class="rounded-full h-80 w-80 flex items-center justify-center border-red-500" style="border-width: 40px;"></div>
        </div>


      </div>

      <div :class="['w-screen min-h-screen']" style="scroll-snap-align: start;scroll-snap-stop: always;" >
        <div class="w-screen min-h-screen flex justify-center items-center">
          
            <div class="m-2 text-8xl font-bold">
            　{{ correctAnswerCount }} / {{ tests.length }}
            </div>
        </div>
      </div>

    </div>
  </div>
</template>

<script>
  import { ref, reactive } from 'vue'
  import { RadioGroup, RadioGroupDescription, RadioGroupLabel, RadioGroupOption } from '@headlessui/vue'

  export default {
    props: {},
    components: {
      RadioGroup,
      RadioGroupDescription,
      RadioGroupLabel,
      RadioGroupOption,
    },
    methods:{
      answer_select(test,choice){
        if(choice.answer) {
          test.correct_answer_flg = true;
          setTimeout(function(){
            test.correct_answer_flg = false;
          }, 1000);
        }
      },
    },
    computed:{
      correctAnswerCount(){
        let n = 0;
        for (let test of this.tests) {
          if(test.selected?.answer){
            n++;
          }
        }
        return n;
      },
    },
    setup(props) {
      const tests = reactive([
        {
          question:"消防法令に定める「関係者」として、誤っているものは次のうちどれか",
          choices:[
            {choice:"防火対象物の管理者",     answer:false},
            {choice:"防火対象物の所有者",     answer:false},
            {choice:"防火対象物の防火管理者", answer:true},
            {choice:"防火対象物の占有者",     answer:false}
          ],
          correct_answer_flg:false, selected:null,
        },
        {
          question:"無窓階の説明として、消防法令上、正しいものは次のうちどれか",
          choices:[
            {choice:"非難上または、消火活動上有効な開口部が一定基準に達しない階", answer:true },
            {choice:"建築物の外壁に窓を有しない階", answer:false},
            {choice:"採光上又は消火活動上有効な窓が一定基準に達しない階", answer:false},
            {choice:"排煙上又は消火活動上有効な窓が一定基準に達しない階", answer:false}
          ],
          correct_answer_flg:false, selected:null,
        },
        {
          question:"無窓階の説明として、消防法令上、正しいものは次のうちどれか",
          choices:[
            {choice:"建築物の外壁に窓を有しない階",answer:false},
            {choice:"非難上または、消火活動上有効な開口部が一定基準に達しない階",answer:true},
            {choice:"採光上又は排煙上有効な開口部を有しない階",answer:false},
            {choice:"消火活動上有効な窓が一定基準に達しない階",answer:false}
          ],
          correct_answer_flg:false, selected:null,
        },
        {
          question:"無窓階の説明として、消防法令上、正しいものは次のうちどれか",
          choices:[
            {choice:"消火活動上有効な窓を有しない階",answer:false},
            {choice:"非難上又は排煙上有効な開口部が一定基準に達しない階",answer:false},
            {choice:"非難上または、消火活動上有効な開口部が一定基準に達しない階",answer:true},
            {choice:"建築物の外壁に窓を有しない階",answer:false}
          ],
          correct_answer_flg:false, selected:null,
        },
        {
          question:"無窓階の説明として、消防法令上、正しいものは次のうちどれか",
          choices:[
            {choice:"消火活動上有効な窓を有しない階",answer:false},
            {choice:"非難上または、消火活動上有効な開口部が一定基準に達しない階",answer:true},
            {choice:"採光上又は排煙上有効な開口部が一定基準に達しない階",answer:false},
            {choice:"窓を有しない階",answer:false}
          ],
          correct_answer_flg:false, selected:null,
        },
        {
          question:"次の記述のうち、消防法令上、誤っているものは次のうちどれか。",
          choices:[
            {choice:"消防用設備等とは、消防の用に供する設備、消防用水及び消火活動上必要な施設をいう",answer:false},
            {choice:"防火対象物の関係者とは、防火対象物の所有者、管理者又は占有者をいう",answer:false},
            {choice:"消防用設備等を設置することが義務付けられている防火対象物は、病院、旅館等不特定多数のものが出入りする防火対象物に限られる",answer:true},
            {choice:"戸建て一般住宅については、消防用設備等の設置義務はない",answer:false}
          ],
          correct_answer_flg:false, selected:null,
        },
        {
          question:"消防用設備等に関する記述として、消防法令上、正しいものは次のうちどれか",
          choices:[
            {choice:"消防用設備等を設置することが義務付けられている防火対象物は、学校、病院、及び旅館等の不特定多数の者が出入りする防火対象物に限られている",answer:false},
            {choice:"戸建て一般住宅についても、一定の規模を超える場合、消防用設備等を設置しなければならない",answer:false},
            {choice:"消防用設備とは、消防の用に供する設備及び消火活動上必要な施設をいう",answer:false},
            {choice:"政令で定める防火対象物の関係者は、政令で定める技術上の基準に従って消防用設備等を設置し、及び維持する義務がある",answer:true}
          ],
          correct_answer_flg:false, selected:null,
        },
        {
          question:"消防法令上、特定防火対象物に該当しないものは、次のうちどれか",
          choices:[
            {choice:"小学校",answer:true},
            {choice:"物品販売店舗",answer:false},
            {choice:"旅館",answer:false},
            {choice:"公衆浴場のうち、蒸気浴場、熱気浴場その他これらに類するもの",answer:false}
          ],
          correct_answer_flg:false, selected:null,
        },
        {
          question:"消防法令上、特定防火対象物に該当するものは、次のうちどれか",
          choices:[
            {choice:"小学校",answer:false},
            {choice:"共同住宅",answer:false},
            {choice:"百貨店",answer:true},
            {choice:"図書館",answer:false}
          ],
          correct_answer_flg:false, selected:null,
        },
        {
          question:"消防法令上、特定防火対象物に該当しないものは、次のうちどれか",
          choices:[
            {choice:"飲食店",answer:false},
            {choice:"映画館",answer:false},
            {choice:"テレビスタジオ",answer:true},
            {choice:"幼稚園",answer:false}
          ],
          correct_answer_flg:false, selected:null,
        },
        {
          question:"消防法令上、特定防火対象物に該当しないものは、次のうちどれか",
          choices:[
            {choice:"百貨店",answer:false},
            {choice:"映画スタジオ",answer:true},
            {choice:"旅館",answer:false},
            {choice:"病院",answer:false}
          ],
          correct_answer_flg:false, selected:null,
        },
        {
          question:"消防法令上、特定防火対象物に該当するのは、次のうちどれか",
          choices:[
            {choice:"図書館と事務所からなる高層ビル",answer:false},
            {choice:"蒸気浴場、熱気浴場その他これらに類する公衆浴場",answer:true},
            {choice:"テレビスタジオが併設された映画スタジオ",answer:false},
            {choice:"冷凍倉庫を含む作業場",answer:false}
          ],
          correct_answer_flg:false, selected:null,
        },
        {
          question:"消防用設備等を設置する場合の防火対象物の基準について、消防法令上、正しいものはどれか",
          choices:[
            {choice:"防火対象物が開口部のない耐火構造の床又は壁で区画されているときは、それぞれ別の防火対象物とみなされる",answer:true},
            {choice:"同一敷地内にある２以上の防火対象物は、原則として一の防火対象物とみなされる",answer:false},
            {choice:"設置することが義務付けられている防火対象物は、百貨店、病院、旅館等不特定多数のものが出入りする防火対象物に限られている",answer:false},
            {choice:"戸建て一般住宅についても一定の規模を超える場合、消防用設備当の設置を義務付けられる場合がある",answer:false}
          ],
          correct_answer_flg:false, selected:null,
        },
        {
          question:"消防用設備等の設置及び維持の技術上の基準の適用について、一の防火対象物でも別の防火対象物とみなされる部分として、消防法令上、正しいものは次のうちどれか",
          choices:[
            {choice:"耐火構造の建物で、特定防火設備である防火戸又は壁で区画された部分",answer:false},
            {choice:"防火構造の床又は壁で区画され、開口部は特定防火設備である防火戸で区画された部分",answer:false},
            {choice:"防火構造の床又は壁で区画され、かつ、開口部にはドレンチャー設備が設けられた部分",answer:false},
            {choice:"開口部のない耐火構造の床又は壁で区画された部分",answer:true}
          ],
          correct_answer_flg:false, selected:null,
        },
        {
          question:"消防用設備等を設置しなければ防火対象物に関する説明として、消防法令上、誤っているものは次のうちどれか",
          choices:[
            {choice:"防火対象物が開口部のない耐火構造の床又は壁で区画されたときは、消防用設備等の設置について、その区画された部分をそれぞれ別の防火対象物みなす",answer:false},
            {choice:"複合用途防火対象物で同一の用途に供される部分は、消防用設備等の設置について、用途の管理者又は階に関係なく一の防火対象物とみなされる場合がある",answer:false},
            {choice:"同一敷地内にある２以上の防火対象物で、外壁間の中心線からの水平距離が１階は３ｍ以下、２階以上は５ｍ以下で近接する場合、消防用設備等の設置について、１棟とみなされる",answer:true},
            {choice:"特定防火対象物の地階で、地下街と一体を成すものとして消防長又は消防署長が指定したものは、消防用設備等の設置について、地下街の一部とみなされる場合がある",answer:false}
          ],
          correct_answer_flg:false, selected:null,
        },
        {
          question:"１階が物品販売店舗、２回が料理店である防火対象物に消防用設備等を設置する場合について、消防法令上、正しいものは次のうちどれか",
          choices:[
            {choice:"１階と２階の管理者が別であれば、それぞれ別の防火対象物とみなすとみなす",answer:false},
            {choice:"１階と２階が耐火構造の床又は壁で区画され、かつ、開口部に特定防火設備である防火戸が設けられていれば、それぞれ別の防火対象物とみなす",answer:false},
            {choice:"階段部分を除き、１階と２階が耐火構造の床又は壁で区画されていれば、それぞれ別の防火対象物とみなす",answer:false},
            {choice:"１階と２階が開口部のない耐火構造の床又は壁で区画されていれば、それぞれ別の防火対象物とみなす",answer:true}
          ],
          correct_answer_flg:false, selected:null,
        },
        {
          question:"消防法令上、一定の防火対象物の関係者は、消防用設備等を設置し、維持することが義務付けられているが、これに関する説明として、正しいものは次のうちどれか",
          choices:[
            {choice:"設置することが義務付けられている防火対象物は、百貨店病院、旅館等の不特定多数の者が出入りする防火対象物に限られる",answer:false},
            {choice:"戸建て一般住宅についても、一定の基準を超える場合、消防用設備等を設置しなければならない",answer:false},
            {choice:"防火対象物の関係者とは、防火対象物の所有者、管理者又は占有者をいう。この関係者で権原を有するものが、設置し維持するべきことに対する命令に違反した場合、処罰の対象となる",answer:true},
            {choice:"消防用設備等とは、消防の用に供する設備、消防用水及び消火活動上必要な施設をいい、水バケツはこれに含まれない",answer:false}
          ],
          correct_answer_flg:false, selected:null,
        },
        {
          question:"消防法令に定められている用語の定義又は説明として、誤っているものは次のうちどれか",
          choices:[
            {choice:"消防の用に供する設備…消火設備、警報設備及び避難設備をいう",answer:false},
            {choice:"消火活動上必要な施設…排煙設備、連結水設備及び動力消防ポンプ設備をいう",answer:true},
            {choice:"防火対象物の関係者…防火対象物の所有者、管理者又は占有者をいう",answer:false},
            {choice:"複合用途防火対象物…政令で定める２以上の用途に供される防火対象物をいう",answer:false}
          ],
          correct_answer_flg:false, selected:null,
        },
        {
          question:"消防用設備等の種類について、消防法令上、誤っているのは次のうちどれか",
          choices:[
            {choice:"動力消防ポンプ設備は、スプリンクラー設備と同じく、消火設備に含まれる",answer:false},
            {choice:"自動火災放置設備は、非常警報設備と同じく、警報設備に含まれる",answer:false},
            {choice:"避難橋は、すべり台や誘導灯と同じく、避難設備に含まれる",answer:false},
            {choice:"消防機関へ通報する火災報知設備は、無線通信補助設備と同じく、消火活動上必要な施設に含まれる",answer:true}
          ],
          correct_answer_flg:false, selected:null,
        },
        {
          question:"消防用設備等の種類について、消防法令上、誤っているのは次のうちどれか",
          choices:[
            {choice:"屋内消火栓設備は、スプリンクラー設備と同じく、消火設備に含まれる",answer:false},
            {choice:"連結送水管は、消火器と同じく、消火設備に含まれる",answer:true},
            {choice:"避難橋は、すべり台や誘導灯と同じく、避難設備に含まれる",answer:false},
            {choice:"漏電火災報知器は、非常警報設備と同じく、警報設備に含まれる",answer:false}
          ],
          correct_answer_flg:false, selected:null,
        },
        {
          question:"消防法令上、「警報設備」に含まれないものは、次のうちどれか",
          choices:[
            {choice:"消防機関へ通報する火災報知設備",answer:false},
            {choice:"手動式サイレン",answer:false},
            {choice:"放送設備",answer:false},
            {choice:"無線通信補助設備",answer:true}
          ],
          correct_answer_flg:false, selected:null,
        },
        {
          question:"消防用設備等の技術上の基準に関する政令若しくはこれに基づく命令の規定が改正されたとき、改正後の規定に適合させなければならない消防用設備として、消防法令上、正しいものは次のうちどれか",
          choices:[
            {choice:"工場に設置されている屋内消火栓設備",answer:false},
            {choice:"展示場に設置されている自動火災報知設備",answer:true},
            {choice:"ラック式倉庫に設置されているスプリンクラー設備",answer:false},
            {choice:"図書館の蔵書室に設置されている二酸化炭素を放射する不活性ガス消火設備",answer:false}
          ],
          correct_answer_flg:false, selected:null,
        },
        {
          question:"用途が事務所である防火対象物において、消防用設備等の技術上の基準に関する政令又はこれに基づく命令の規定が改正されたとき、改正後の規定に適合させなければならない消防用設備等として、消防法令上、誤っているものは次のうちどれか。ただし、防火対象物の構造、用途、規模の変更はないものとする",
          choices:[
            {choice:"消火器",answer:false},
            {choice:"避難器具",answer:false},
            {choice:"屋内消火栓設備",answer:true},
            {choice:"誘導灯",answer:false}
          ],
          correct_answer_flg:false, selected:null,
        },
        {
          question:"防火対象物の増築に関する次の記述のうち、文中の（　）に当てはまる数値として、消防法令上、正しいものはどれか「設備等技術基準の施工又は適用の際、既に存する特定防火対象物以外の防火対象物における消防用設備等（消火器、避難器具その他政令で定めるものを除く）がこれらの規定に適合せず、当該規定が適用をされていないとき、当該防火対象物を増築した場合、基準時以降の増築部分の床面積の合計が（　）㎡となるものは、当該消防用設備等を当該規定に適合させなければならない。ただし、当該消防設備等は、従前の規定に適合しており、工事の着手は基準時以降であって、増築部分の床面積の合計が、基準時における当該対象物の延べ面積の２分の１以上とならないものである",
          choices:[
            {choice:"300",answer:false},
            {choice:"500",answer:false},
            {choice:"700",answer:false},
            {choice:"1000",answer:true}
          ],
          correct_answer_flg:false, selected:null,
        },
        {
          question:"防火対象物を消防用設備等の技術上の基準が改正された後に増築又は改築した場合、消防設備等を改正後の基準に適合させなければならない増築又は改築の規模として、消防法令上ただしいものは次のうちどれか",
          choices:[
            {choice:"増築に関わる当該防火対象物の床面積の合計が、増築前の延べ面積の1/3となる場合",answer:false},
            {choice:"改築に関わる当該防火対象物の床面積の合計が1000㎡となる場合",answer:true},
            {choice:"増築に関わる当該防火対象物の床面積の合計が500㎡となる場合",answer:false},
            {choice:"増築又は改築以前の当該防火対象物の延べ面積と、増築又は改築後の延べ面積との差が500㎡となる場合",answer:false}
          ],
          correct_answer_flg:false, selected:null,
        },
        {
          question:"消防用設備等の技術上の基準が改正された後に防火対象物を増築又は改築した場合で、消防用設備等を改正後の基準にてきごうさせなければならないものとして、消防法令上、正しいものは次のうちどれか",
          choices:[
            {choice:"延べ面積が1,000㎡の工場を1,500㎡に増築する",answer:true},
            {choice:"延べ面積が1,500㎡の倉庫を2,000㎡に増築する",answer:false},
            {choice:"延べ面積が2,500㎡の図書館のうち700㎡を改築する",answer:false},
            {choice:"延べ面積が3,000㎡の中学校のうち800㎡を改築する",answer:false}
          ],
          correct_answer_flg:false, selected:null,
        },
        {
          question:"既存の防火対象物における消防用設備等は、設備等に関する法令の改正があっても、原則として、改正前の基準に適合していればよいと規定されているが、法令の改正後に一定の「増改築」が行われた場合は、この規定は適用されず、改正後の基準に適合させなければならない。この一定の「増改築」に該当しないものは、次のうちどれか",
          choices:[
            {choice:"既存の延べ面積の1/3で800㎡の増改築",answer:true},
            {choice:"既存の延べ面積の1/4で1299㎡の増改築",answer:false},
            {choice:"既存の延べ面積の3/5で500㎡の増改築",answer:false},
            {choice:"既存の延べ面積の5/6で1,500㎡の増改築",answer:false}
          ],
          correct_answer_flg:false, selected:null,
        },
        {
          question:"既存の防火対象物を消防用設備等の技術上の基準が改正された後に増築、改築又は修繕若しくは模様替えをした場合、消防用設備等を改正後の基準に適合させなければならない増築、改築または修繕もしくは模様替えに該当するものとして、消防法令上、正しいものは次のうちどれか",
          choices:[
            {choice:"延べ面積が1,000㎡の倉庫を1,200㎡に増築する",answer:false},
            {choice:"延べ面積が1,500㎡の工場のうち500㎡を改築する",answer:false},
            {choice:"延べ面積が2,000㎡の遊技場の主要構造部である壁を2/3にわたって模様替えする",answer:true},
            {choice:"延べ面積が2,500㎡の劇場を主要構造部である壁を1/3にわたって修繕する",answer:false}
          ],
          correct_answer_flg:false, selected:null,
        },
        {
          question:"防火対象物の用途が変更された場合の消防用設備等の技術上の基準の適用について、消防法令上、正しいものは次のうちどれか。",
          choices:[
            {choice:"防火対象物の用途が変更された場合は、変更後の用途に適合する消防用設備等を設置しなければならない",answer:false},
            {choice:"変更後の用途が特定防火対象物に該当しなければ、すべての消防用設備等を変更しなくて良い",answer:false},
            {choice:"変更後の用途が特定防火対象物に該当する場合は、変更後の用途区分に適合する消防用設備等を設置しなければならない",answer:true},
            {choice:"用途変更前に設置された消防用設備等が違反していた場合は、変更前の基準に適合するよう措置しなければならない",answer:false}
          ],
          correct_answer_flg:false, selected:null,
        },
        {
          question:"防火対象物の用途変更と消防用設備等（消火器、避難器具その他政令で定めるものを除く。）の技術基準の関係について、消防法令上、正しいものは次のうちどれか",
          choices:[
            {choice:"消防用設備等が変更前の用途に関わる技術基準に違反していた場合、変更後の用途に関わる技術基準にしたがって設置しなければならない",answer:true},
            {choice:"用途が変更された場合、いかなる用途の防火対象物であっても変更後の用途に係る技術基準に従い設置しなければならない",answer:false},
            {choice:"用途が変更されて特定防火対象物になった場合、変更前の用途に係る技術基準に従って設置されていれば、変更後の用途基準に従って設置する必要はない",answer:false},
            {choice:"用途が変更された後に、主要構造部である壁について過半の修繕を施した場合、変更前の用途に係る技術基準に従って設置されれば、変更後の用途に係る技術基準に従って設置する必要はない",answer:false}
          ],
          correct_answer_flg:false, selected:null,
        },
        {
          question:"防火対象物の用途が変更された場合の消防用設備等の技術上の基準の適用について、消防法令上、誤っているものは次のうちどれか",
          choices:[
            {choice:"原則として、用途変更前に設置された消防用設備等はそのままにしておいてよいが、その後、一定規模以上の増改築工事を行う場合は、変更後の用途区分に適合する消防用設備等を設置しなければならない",answer:false},
            {choice:"用途変更前に設置された消防用設備等が基準に違反していた場合は、用途変更後の基準に適合する消防用設備等を設置しなければならない",answer:false},
            {choice:"変更後の用途が特定防火対象物に該当する場合は、変更後の用途区分に適合する消防用設備等を設置しなければならない",answer:false},
            {choice:"用途変更後に不要となった消防用設備等については、撤去する等確実に機能を停止させなければならない",answer:true}
          ],
          correct_answer_flg:false, selected:null,
        },
        {
          question:"消防用設備等の定期点検を消防設備士又は消防設備点検資格者にさせなければならない防火対象物として、消防法令上、正しいものは次のうちどれか。ただし、消防庁又は消防署長が火災予防上必要があると認めてしていするものを除く",
          choices:[
            {choice:"すべての防火対象物",answer:false},
            {choice:"すべての特定防火対象物",answer:false},
            {choice:"特定防火対象物で延べ面積が1,000㎡以上のもの",answer:true},
            {choice:"特定防火対象物以外の防火対象物で、延べ面積が2,000㎡以上のもの",answer:false}
          ],
          correct_answer_flg:false, selected:null,
        },
        {
          question:"消防用設備等の定期点検を消防設備士又は消防設備点検資格者にさせなければならない防火対象物として、消防法令上、正しいものは次のうちどれか。ただし、消防長又は消防署長がしていするものを除く",
          choices:[
            {choice:"ホテルで、延べ面積が500㎡のもの",answer:false},
            {choice:"映画館で、延べ面積が700㎡のもの",answer:false},
            {choice:"キャバレーで、延べ面積が1,000㎡のもの",answer:true},
            {choice:"駐車場で、延べ面積が1,500㎡のもの",answer:false}
          ],
          correct_answer_flg:false, selected:null,
        },
        {
          question:"消防設備士又は消防設備点検資格者に、消防用設備等を定期に点検させ、その結果を消防長又は消防署長報告しなければならない防火対象物として、消防法令上、正しいものは次のうちどれか",
          choices:[
            {choice:"すべての高層建築物",answer:false},
            {choice:"キャバレーで、延べ面積が500㎡のもの",answer:false},
            {choice:"病院で、延べ面積が1,000㎡のもの",answer:true},
            {choice:"すべての旅館",answer:false}
          ],
          correct_answer_flg:false, selected:null,
        },
        {
          question:"消防用設備等は定期的に点検し、その結果を一定期間ごとに消防長又は消防署長に報告しなければならないが、防火対象物の用途と報告の期間の組み合わせとして、消防法令上、正しいものを答えなさい",
          choices:[
            {choice:"保育所・・・３年に１回",answer:false},
            {choice:"幼稚園・・・３年に１回",answer:false},
            {choice:"劇場・・・６カ月に１回",answer:false},
            {choice:"物品販売店舗・・・１年に１回",answer:true},
          ],
          correct_answer_flg:false, selected:null,
        },
        {
          question:"消防用設備等は定期的に点検し、その結果を一定期間ごとに消防長又は消防署長に報告しなければならないが、防火対象物の用途と報告の期間の組み合わせとして、消防法令上、正しいものを答えなさい",
          choices:[
            {choice:"養護老人ホーム・・・１年に１回",answer:true},
            {choice:"小学校・・・１年に１回",answer:false},
            {choice:"百貨店・・・６カ月に１回",answer:false},
            {choice:"駐車場・・・１年に１回",answer:false}
          ],
          correct_answer_flg:false, selected:null,
        },
        {
          question:"消防用設備等の定期点検を消防設備士又は消防設備点検資格者にさせなければならない特定防火対象物の最小の延べ面積として、消防法令に定められているものは次のうちどれか",
          choices:[
            {choice:"300㎡",answer:false},
            {choice:"500㎡",answer:false},
            {choice:"1,000㎡",answer:true},
            {choice:"2,000㎡",answer:false}
          ],
          correct_answer_flg:false, selected:null,
        },
        {
          question:"消防法令上、消防用設備等の定期点検を、消防設備士または消防設備点検資格者にさせなければならない特定防火対象物は、次のうちどれか",
          choices:[
            {choice:"ホテルで、延べ面積が500㎡のもの",answer:false},
            {choice:"映画館で、延べ面積が700㎡のもの",answer:false},
            {choice:"幼稚園で、延べ面積が800㎡のもの",answer:false},
            {choice:"飲食店で、延べ面積が1,000㎡のもの",answer:true}
          ],
          correct_answer_flg:false, selected:null,
        },
        {
          question:"消防用設備等の定期点検を消防設備士又は消防設備点検資格者にさせなければならない防火対象物として、消防法令上、正しいものは次のうちどれか。ただし、いずれの防火対象物も消防庁又は消防署長の指定を受けていないものとする",
          choices:[
            {choice:"共同住宅で、延べ面積が2,000㎡のもの",answer:false},
            {choice:"小学校で、延べ面積が1,000㎡のもの",answer:false},
            {choice:"百貨店で、延べ面積が1,000㎡のもの",answer:true},
            {choice:"旅館で、延べ面積が500㎡のもの",answer:false}
          ],
          correct_answer_flg:false, selected:null,
        },
        {
          question:"消防用設備の定期点検及び報告に関する記述について、消防法令上、誤っているものは次のうちどれか。ただし、総務省令で定める舟車を除く。",
          choices:[
            {choice:"消防法第17条に基づいて設置された消防用設備等は、定期に点検をしなければならない",answer:false},
            {choice:"特定防火対象物以外の防火対象物にあっては、点検を行った結果を維持台帳に記録し、消防長又は消防署長に報告を求められたときに報告すればよい",answer:true},
            {choice:"特定防火対象物の関係者は、点検の結果を消防長又は消防署長に報告しなければならない",answer:false},
            {choice:"延べ面積が1,000㎡以上の特定防火対象物の消防用設備等にあっては、消防設備士又は消防設備点検資格者に点検をさせなければならない",answer:false}
          ],
          correct_answer_flg:false, selected:null,
        },
        {
          question:"消防用設備等の点検及び報告に関する記述として、消防法令上、正しいものは次のうちどれか",
          choices:[
            {choice:"消防用設備等の点検結果については、消防長又は消防署長から報告を求められたときに報告すればよい",answer:false},
            {choice:"店舗に任意に設置された消防用設備等であっても一定期間ごとに点検し、その結果を報告しなければならない",answer:false},
            {choice:"延べ面積が1,000㎡以上の病院に設置された法令上設置義務のある消防用設備等の点検は、消防設備士または消防設備点検資格者に行わせなければならない",answer:true},
            {choice:"点検を行った消防設備士は、消防用設備等の点検結果について消防長又は消防署長に報告しなければならない",answer:false}
          ],
          correct_answer_flg:false, selected:null,
        },
        {
          question:"消防用設備等（簡易消火用具及び非常警報器具を除く）を設置したときの届出及び検査について、消防法令上、誤っているものは次のうちどれか",
          choices:[
            {choice:"特定防火対象物以外の防火対象物に設置した消防用設備等であっても、消防長又は消防署長へ届け出て検査をうけなければならない場合がある",answer:false},
            {choice:"消防用設備等を設置したときに、届け出て検査を受けるのは、当該防火対象物の関係者である",answer:false},
            {choice:"延べ床面積が300㎡以上の特定防火対象物に消防法第17条に基づき設置した消防用設備等については、消防長又は消防署長へ届け出て検査をうけなければならない",answer:false},
            {choice:"消防用設備等を設置したときに届け出て検査を受けるのは当該防火対象物の工事を行った工事責任者である",answer:true}
          ],
          correct_answer_flg:false, selected:null,
        },
        {
          question:"設備等技術基準に従って設置しなければならない消防用設備等（簡易消火用具及び非常警報器具を除く）を設置した場合、消防長又は消防署長に届け出て、検査をうけなければならない防火対象物として、消防法令上、正しいものを答えなさい。ただし、特定１階段等防火対象物でないものとする",
          choices:[
            {choice:"入院施設を有しない助産所で、延べ面積が250㎡のもの",answer:false},
            {choice:"集会場で、延べ面積が250㎡のもの",answer:false},
            {choice:"教会で、延べ面積が250㎡のもの",answer:false},
            {choice:"カラオケボックスで、延べ面積が250㎡のもの",answer:true}
          ],
          correct_answer_flg:false, selected:null,
        },
        {
          question:"設備等技術基準に従って設置しなければならない消防用設備等（簡易消火用具及び非常警報器具を除く）を設置した場合、消防長又は消防署長に届け出て、検査をうけなければならない防火対象物として、消防法令上、正しいものを答えなさい。ただし、特定１階段等防火対象物でないものとする",
          choices:[
            {choice:"入院施設を有しない助産所で、延べ面積が250㎡のもの",answer:false},
            {choice:"集会場で、延べ面積が250㎡のもの",answer:false},
            {choice:"教会で、延べ面積が250㎡のもの",answer:false},
            {choice:"ナイトクラブで、延べ面積が500㎡のもの",answer:true}
          ],
          correct_answer_flg:false, selected:null,
        },
        {
          question:"消防用設備等を設備等技術基準に従って設置した場合、消防法令上、消防機関の検査をうけなくてもよい防火対象物は次のうちどれか。ただし、防火対象物はすべて平屋建てで、非常警報器具及び簡易消火用具は設置されていないものとする",
          choices:[
            {choice:"延べ面積200㎡の老人短期入所施設",answer:false},
            {choice:"延べ面積250㎡の特別支援学校",answer:true},
            {choice:"延べ面積350㎡の診療所",answer:false},
            {choice:"延べ面積500㎡の演芸場",answer:false}
          ],
          correct_answer_flg:false, selected:null,
        },
        {
          question:"消防用設備等の設置届に基づく検査について、消防法令上、誤っているものは次のうちどれか",
          choices:[
            {choice:"特定防火対象物で延べ面積が300㎡以上ある場合は、検査を受けなければならない",answer:false},
            {choice:"特定防火対象物以外の防火対象物で延べ面積が300㎡以上のもののうち、消防超又は消防署長が火災予防上必要あると認めて指定する場合は、検査を受けなければならない",answer:false},
            {choice:"消防用設備等のうち簡易消火用具及び非常警報器具は、検査の対象から除かれている。",answer:false},
            {choice:"検査を受けなければならない特定防火対象物の関係者は、消防用設備等の設置に係る工事が完了した日から１０日以内に消防長又は消防署長に届け出なければならない",answer:true}
          ],
          correct_answer_flg:false, selected:null,
        },
        {
          question:"消防用設備等を技術基準に従って設置した場合、消防長又は消防署長に届出て検査を受けなくてもよい防火対象物として、消防法令上、正しいものは次のうちどれか。ただし、当該防火対象物の避難階は１階であり、階段は屋内にのみ設けられ、総務省令で定める避難上有効な構造を有していないものとする",
          choices:[
            {choice:"地上に直通する階段が１か所ある２階建てでの旅館で、延べ面積が100㎡のもの",answer:false},
            {choice:"地上に直通する階段が１か所ある３階建ての飲食店で、延べ面積が150㎡のもの",answer:false},
            {choice:"地上に直通する階段が２か所ある４階建ての入院施設のある診療所で、延べ面積が200㎡のもの",answer:false},
            {choice:"地上に直通する階段が２か所ある５階建ての作業場で、延べ面積が250㎡のもの",answer:true}
          ],
          correct_answer_flg:false, selected:null,
        },
        {
          question:"工事整備対象設備等の着工届について、消防法令上、正しいものは次のうちどれか",
          choices:[
            {choice:"防火対象物の関係者が、工事に着手しようとする日の10日前までに都道府県知事に届け出る",answer:false},
            {choice:"甲種消防設備士が、工事に着手しようとする日の10日前までに消防長又は消防署長に届け出る",answer:true},
            {choice:"甲種消防設備士が、工事に着手しようとする日の7日前までに消防長又は消防署長に届け出る",answer:false},
            {choice:"防火対象物の関係者が、工事に着工しようとする日の７日前までに消防長又は消防署長に届け出る",answer:false}
          ],
          correct_answer_flg:false, selected:null,
        },
        {
          question:"工事設備対象設備等の工事の届出について、消防法令上、正しいものは次のうちどれか",
          choices:[
            {choice:"甲種消防設備士は、消防用設備等の工事に着手しようとする場合、消防長又は消防署長に必要な事項について届け出なければならない",answer:true},
            {choice:"防火対象物の関係者は、消防用設備等の工事に着手しようとする場合、消防長又は、消防署長に必要な事項について届け出なければならない",answer:false},
            {choice:"甲種消防設備士は、消防用設備等の工事に着手したときは、遅滞なく消防長又は、消防署長に必要な事項について届け出なければならない",answer:false},
            {choice:"防火対象物の関係者は、消防用設備等の工事に着手したときは、遅滞なく消防長又は消防署長に必要な事項について届け出なければならない",answer:false}
          ],
          correct_answer_flg:false, selected:null,
        },
        {
          question:"工事整備対象設備等の着工届について、消防法令上、正しいものは次のうちどれか",
          choices:[
            {choice:"甲種消防設備士は、工事に着手しようとする場合、工事整備対象設備等着工届出書を10日前までに都道府県知事に提出しなければならない",answer:false},
            {choice:"特定防火対象物の関係者は、工事に着手しようとする場合、工事整備対象設備等着工届出書を10日前までに都道府県知事に提出しなければならない",answer:false},
            {choice:"甲種消防設備士は、工事に着手しようとする場合、工事設備対象設備等着工届出書を10日前までに消防長又は消防署長に提出しなければならない",answer:true},
            {choice:"特定防火対象物の関係者は、工事に着手しようとする場合、工事整備対象設備等着工届を10日前までに消防長又は消防署長に提出しなければならない",answer:false}
          ],
          correct_answer_flg:false, selected:null,
        },
        {
          question:"消防用設備等の設置維持命令に関する次の記述のうち、文中の（　）に当てはまる語句の組み合わせとして、消防法令上、正しいものは次のうちどれか。「（ア）は、防火対象物における消防用設備等が（イ）に従って設置され、又は維持されていないと認める時は、当該防火対象物の関係者で（ウ）に対し、（イ）に従ってこれを設置すべきこと、又はその維持のため、必要な措置をなすべきことを命ずることができる」",
          choices:[
            {choice:"（ア）消防長又は消防署長、（イ）設備等技術基準、（ウ）権原を有する者",answer:true},
            {choice:"（ア）都道府県知事、（イ）設備等設置維持計画、（ウ）防火管理者",answer:false},
            {choice:"（ア）消防長又は消防署長、（イ）設備等設置維持計画、（ウ）権原を有する者",answer:false},
            {choice:"（ア）都道府県知事、（イ）設備等技術基準、（ウ）防火管理者",answer:false}
          ],
          correct_answer_flg:false, selected:null,
        },
        {
          question:"消防用設備等の設置又は維持に関する命令について、消防法令上、正しいものは次のうちどれか",
          choices:[
            {choice:"消防長又は消防署長は、消防用設備等が技術基準に従って維持されていない場合、防火対象物の関係者で権原を有する者に対して、必要な措置をとることを命ずることができる",answer:true},
            {choice:"消防長又は消防署長は、消防用設備等が技術基準に従って設置されていない場合、工事に当たった消防設備士に対して、工事の手直しを命ずることができる",answer:false},
            {choice:"設置の命令に違反して消防用設備等を設置しなかった者は、罰金又は拘留に処される",answer:false},
            {choice:"維持の命令に違反して消防用設備等の維持のため必要な措置をとらなかったものは、懲役又は罰金に処される",answer:false}
          ],
          correct_answer_flg:false, selected:null,
        },
        {
          question:"消防用設備等が技術上の基準に適合していない場合、必要な措置を行うよう命令を受けるものとして、消防法令上、正しいものは次のうちどれか",
          choices:[
            {choice:"防火対象物の管理者で権原を有するもの",answer:true},
            {choice:"防火対象物の占有者",answer:false},
            {choice:"防火対象物の消防用設備等を工事した消防設備士",answer:false},
            {choice:"防火対象物の消防用設備等を点検した消防設備士",answer:false}
          ],
          correct_answer_flg:false, selected:null,
        },
        {
          question:"消防用設備等が技術上の基準に適合していない場合、必要な措置を行うよう命令を受けるものとして、消防法令上、誤っているものは次のうちどれか",
          choices:[
            {choice:"命令は任意に設置した消防用設備等までは及ばない",answer:false},
            {choice:"消防用設備等の設置義務がある防火対象物に消防用設備等の一部が設置されていない場合でも命令のい対象となる",answer:false},
            {choice:"命令を発することができる者は、消防長又は消防署長である",answer:false},
            {choice:"命令の相手方は、防火対象物の関係者であれば当該消防用設備等について権原を有しなくても良い",answer:true}
          ],
          correct_answer_flg:false, selected:null,
        },
        {
          question:"工事整備対象設備等着工届書による届出が必要となる消防用設備として、消防法令上、正しいものは次のうちどれか",
          choices:[
            {choice:"誘導灯",answer:false},
            {choice:"消防機関へ通報する火災報知器",answer:true},
            {choice:"非常警報設備",answer:false},
            {choice:"漏電火災警報器",answer:false}
          ],
          correct_answer_flg:false, selected:null,
        },
        {
          question:"消防設備士でなければ工事又は整備を行うことができない消防用設備等の組み合わせとして、消防法令上、正しいものは次のうちどれか",
          choices:[
            {choice:"屋内消火栓設備、不活性ガス消火設備、スプリンクラー設備、動力消防ポンプ設備",answer:false},
            {choice:"泡消火設備、粉末消火設備、パッケージ型消火設備",answer:true},
            {choice:"自動火災報知設備、漏電火災警報器、放送設備",answer:false},
            {choice:"消火器、救助袋、すべり台、緩降機(かんこうき)",answer:false}
          ],
          correct_answer_flg:false, selected:null,
        },
        {
          question:"消防設備士でなくても行うことができる消防用設備等の整備の範囲として、消防法令上、誤っているものは次のうちどれか",
          choices:[
            {choice:"給水装置工事主任技術者であるAは、スプリンクラー設備の水源に水を補給するための給水管を交換した",answer:false},
            {choice:"電気主任技術者であるＢは、自動火災報知設備の電源表示ランプを交換した",answer:false},
            {choice:"電気工事士であるＣは、屋内消火栓の表示灯が消えていたので、表示灯配線の異常の有無について検査して、電球を取り替えた",answer:false},
            {choice:"水道工事業者であるＤは、屋外消火栓の水漏れ補修を頼まれ、水漏れの原因となった屋外消火栓開閉弁を新品と交換した",answer:true}
          ],
          correct_answer_flg:false, selected:null,
        },
        {
          question:"消防法第17条第２項に規定されている付加条例について、最も適切なものは次のうちどれか",
          choices:[
            {choice:"市町村の付加条例によって、消防用設備等の設置及び維持に関する技術上の基準について、政令で定める基準を強化することができる",answer:true},
            {choice:"市町村の付加条例によって、消防用設備等の設置及び維持に関する技術上の基準について、政令で定める基準を緩和することができる",answer:false},
            {choice:"市町村の付加条例によって、消防法施行令別表第一の防火対象物以外の防火対象物に対して消防用設備等の設置を義務付けることができる",answer:false},
            {choice:"市町村の付加条例によって、政令で定める消防用設備等の一部を設置しなくてもよいという特例基準を定めることができる",answer:false}
          ],
          correct_answer_flg:false, selected:null,
        },
        {
          question:"消防設備士が行うことができる工事又は整備について、消防法令上、誤っているものは次のうちどれか",
          choices:[
            {choice:"甲種特類消防設備士免状の交付を受けている者は、消防用設備等のすべて及び特殊消防用設備等について、整備を行うことができる",answer:true},
            {choice:"甲種第４類消防設備士免状の交付を受けている者は、危険物製造所等に設置する自動的に作動する火災報知設備の工事を行うことができる",answer:false},
            {choice:"乙種第１類消防設備士免状の交付を受けている者は、屋外消火栓設備の開閉弁の整備を行うことができる",answer:false},
            {choice:"乙種第５類消防設備士免状の交付を受けている者は、緩降機本体及びその取付け具の整備を行うことができる",answer:false}
          ],
          correct_answer_flg:false, selected:null,
        },
        {
          question:"消防設備士が行うことができる工事又は整備について、消防法令上、誤っているものは次のうちどれか",
          choices:[
            {choice:"甲種第１類の消防設備士は、スプリンクラー設備の整備を行うことができる",answer:false},
            {choice:"甲種第２類の消防設備士は、泡消火設備の工事を行うことができる",answer:false},
            {choice:"甲種第４類の消防設備士は、漏電火災警報器の整備を行うことができる",answer:true},
            {choice:"乙種第３類の消防設備士は、粉末消火設備の整備を行うことができる",answer:false}
          ],
          correct_answer_flg:false, selected:null,
        },
        {
          question:"消防設備士が行う工事又は整備について、消防法令上、誤っているものは次のうちどれか",
          choices:[
            {choice:"甲種第５類の消防設備士免状の交付を受けている者は、級降機及び救助袋の工事を行うことができる",answer:false},
            {choice:"乙種第４類の消防設備士免状の交付を受けている者は、ガス漏れ火災警報設備の整備を行うことができる",answer:false},
            {choice:"乙種第２類の消防設備士免状の交付を受けている者は、泡消火設備の整備を行うことができる",answer:true},
            {choice:"乙種第１類の消防設備士免状の交付を受けている者は、水噴霧消火設備の工事を行うことができる",answer:false}
          ],
          correct_answer_flg:false, selected:null,
        },
        {
          question:"消防設備士が行う工事又は整備について、消防法令上、正しいものは次のうちどれか",
          choices:[
            {choice:"甲種第１類の消防設備士は、泡消火設備の整備を行うことができる",answer:false},
            {choice:"乙種第５類の消防設備士は、金属製避難はしごの設置工事を行うことができる",answer:false},
            {choice:"甲種第４類の消防設備士は、自動火災報知機設備の設置工事を行うことができる",answer:true},
            {choice:"乙種第６類の消防設備士は、漏電火災警報器の整備を行うことができる",answer:false}
          ],
          correct_answer_flg:false, selected:null,
        },
        {
          question:"消防設備士に関する記述として、消防法令上、誤っているものは次のうちどれか",
          choices:[
            {choice:"消防設備等の移設には、乙種消防設備士の資格を必要とする場合がある",answer:true},
            {choice:"消防用設備等の増設には、甲種消防設備士の資格を必要とする場合がある",answer:false},
            {choice:"消防用設備等の不良個所が指定された場合の不良機器の調整、又は部品交換には、乙種消防設備士の資格を必要とする場合がある",answer:false},
            {choice:"消防用設備等の新設には、甲種消防設備士の資格を必要とする場合がある",answer:false}
          ],
          correct_answer_flg:false, selected:null,
        },
        {
          question:"消防設備士免状に関する記述について、消防法令上正しいものは次のうちどれか",
          choices:[
            {choice:"消防設備士免状の交付を受けた都道府県以外で業務に従事するときは、業務地を管轄する都道府県知事に免状の書換えを申請しなければならない",answer:false},
            {choice:"消防設備士免状の記載事項に変更が生じた場合、当該免状を交付した都道府県知事又は移住地若しくは勤務地を管轄する都道府県知事に免状の書き換えを申請しなければならない",answer:true},
            {choice:"消防設備士免状を亡失したときは、亡失した日から10日以内に免状の再交付を申請しなければならない",answer:false},
            {choice:"消防設備士免状の返納を命ぜられた日から３年を経過しない者については、新たな試験に合格しても免状が交付されないことがある",answer:false}
          ],
          correct_answer_flg:false, selected:null,
        },
        {
          question:"消防設備士免状に関して、消防法令上、誤っているものは次のうちどれか",
          choices:[
            {choice:"消防設備士免状の記載事項に変更を生じたときは、免状を交付した都道府県知事又は移住地若しくは勤務地を管轄する都道府県知事に免状の書換えを申請しなければならない",answer:false},
            {choice:"消防設備士免状をなくした時は、亡失に気づいた日から10日以内に免状を交付した都道府県知事に免状の再交付を申請しなければならない",answer:true},
            {choice:"消防設備士免状を汚損又は破損した者は、免状を交付した都道府県知事に免状の再交付を申請することができる",answer:false},
            {choice:"消防設備士免状の返納命令に違反した者は、罰金又は拘留に処せられることがある",answer:false}
          ],
          correct_answer_flg:false, selected:null,
        },
        {
          question:"消防設備士免状の書き換えについて、消防法令上、正しいものはどれか",
          choices:[
            {choice:"免状に貼ってある写真が撮影した日から10年を超えた場合は、移住地又は勤務地を管轄する消防長又は消防署長に書換の申請をしなければならない",answer:false},
            {choice:"移住地に変更が生じた場合は、移住地又は勤務地を管轄する都道府県知事に書換えの申請をしなければならない",answer:false},
            {choice:"氏名に変更が生じた場合は、免状を交付した都道府県知事又は移住地若しくは勤務地を管轄する都道府県知事に書換の申請をしなければならない",answer:true},
            {choice:"本籍地の属する都道府県に変更が生じた場合は、新たな本籍地を管轄する消防長又は消防署長に書換えの申請をしなければならない",answer:false}
          ],
          correct_answer_flg:false, selected:null,
        },
        {
          question:"消防設備士免状を亡失した場合の再交付申請先として、消防法令上、正しいものは次のうちどれか",
          choices:[
            {choice:"移住地又は勤務地を管轄する都道府県知事",answer:false},
            {choice:"移住地又は勤務地を管轄する消防長又は消防署長",answer:false},
            {choice:"当該免状の交付又は書換をした都道府県知事",answer:true},
            {choice:"当該免状の交付又は書換をした消防長又は消防署長",answer:false}
          ],
          correct_answer_flg:false, selected:null,
        },
        {
          question:"消防設備士免状を亡失してその再交付を受けた者が、亡失した免状を発見した場合は、これを一定期間以内に免状の再交付をした都道府県知事に提出しなければならないとするが、その期間として、消防法令上、正しいものは次のうちどれか",
          choices:[
            {choice:"7日以内",answer:false},
            {choice:"10日以内",answer:true},
            {choice:"14日以内",answer:false},
            {choice:"20日以内",answer:false}
          ],
          correct_answer_flg:false, selected:null,
        },
        {
          question:"消防設備士免状に関する申請とその申請先について、消防法令上、誤っているものの組み合わせは次のうちどれか",
          choices:[
            {choice:"申請：書換え、申請先：移住地又は勤務地を管轄する都道府県知事",answer:false},
            {choice:"申請：再交付、申請先：免状を交付した都道府県知事",answer:false},
            {choice:"申請：書換え、申請先：免状を交付した都道府県知事",answer:false},
            {choice:"申請：再交付、申請先：移住地又は勤務地を管轄する都道府県知事",answer:true}
          ],
          correct_answer_flg:false, selected:null,
        },
        {
          question:"消防設備士免状の記載事項について、消防法令に定めれられていないものは、次のうちどれか",
          choices:[
            {choice:"免状の交付年月日及び交付番号",answer:false},
            {choice:"氏名及び生年月日",answer:false},
            {choice:"現住所",answer:true},
            {choice:"過去１０年いないに執拗した写真",answer:false}
          ],
          correct_answer_flg:false, selected:null,
        },
        {
          question:"次の文中の（　）に当てはまる数値及び語句の組み合わせとして、消防法令上に定められているものは次のうちどれか「消防設備士免状を亡失してその再交付を受けた者は亡失した免状を発見した場合には、これを（ア）日以内に免状の再交付をした（イ）に提出しなければならない",
          choices:[
            {choice:"（ア） 10、（イ）都道府県知事",answer:true},
            {choice:"（ア）10、（イ）消防長又は消防署長",answer:false},
            {choice:"（ア）14、（イ）都道府県知事",answer:false},
            {choice:"（ア）14、（イ）消防長又は消防署長",answer:false}
          ],
          correct_answer_flg:false, selected:null,
        },
        {
          question:"都道府県知事（総務大臣が指定する市町村長その他の機関を含む）が行う工事整備対象設備等の工事又は整備に関する講習について、消防法令上、誤っているものは次のうちどれか",
          choices:[
            {choice:"消防設備士免状の交付を受けた日から5年以内ごとに受講しなければならない",answer:true},
            {choice:"工事整備対象設備等の工事又は整備に従事していない消防設備士もじゅこうしなければならない",answer:false},
            {choice:"消防設備士免状の種類及び指定区分等に応じて行われる",answer:false},
            {choice:"定められた期間内に受講しなければ、消防設備士免状の返納を命ぜられることがある",answer:false}
          ],
          correct_answer_flg:false, selected:null,
        },
        {
          question:"都道府県知事（総務大臣が指定する市町村その他の機関を含む）が行う工事整備対象設備等の工事又は整備に関する講習制度について、消防法令上、正しいものは次のうちどれか",
          choices:[
            {choice:"消防設備士は、その業務に従事することになった日以降における最初の４月１日から５年以内ごとに講習をうけなければならない",answer:false},
            {choice:"消防設備士は、免状の交付を受けた日以降における最初の４月１日から５月１日から２年以内に講習を受け、その後、前回の講習を受けなければならない",answer:false},
            {choice:"消防設備士は、その業務に従事することになった日以降における最初の４月１日から２年以内に講習を受け、その後、前回の講習を受けた日以降における最初の４月１日から５年いないごとに講習をうけなければならない",answer:false},
            {choice:"消防設備士は、免状の交付を受けた日以降における最初の４月１日から２年以内に講習を受け、その後、前回の講習を受けた日以降における最初の４月１日から５年以内ごとに講習を受けなければならない",answer:true}
          ],
          correct_answer_flg:false, selected:null,
        },
        {
          question:"工事整備対象設備等の工事又は整備に関する講習の実施者として、消防法令上正しいものは次のうちどれか",
          choices:[
            {choice:"都道府県知事",answer:true},
            {choice:"総務大臣",answer:false},
            {choice:"消防長又は消防署長",answer:false},
            {choice:"消防長長官",answer:false}
          ],
          correct_answer_flg:false, selected:null,
        },
        {
          question:"都道府県知事（総務大臣が指定する市町村長その他の機関を含む）が行う工事整備対象設備等の工事又は整備に関する講習の受講時期について、消防法令で定められているものは、次のうちどれか",
          choices:[
            {choice:"免状の交付を受けた日から３年以内ごと",answer:false},
            {choice:"免状の交付を受けた日から５年以内ごと",answer:false},
            {choice:"免状の交付を受けた日から２年以内、その後、前回の講習を受けた日から５年以内ごと",answer:false},
            {choice:"免状の交付を受けた日以降における最初の４月１日から２年以内、その後、前回の講習を受けた日以降における最初の４月１日から５年以内ごと",answer:true}
          ],
          correct_answer_flg:false, selected:null,
        },
        {
          question:"都道府県知事（総務大臣が指定する市町村長その他の機関を含む）が行う工事整備対象設備等の工事又は整備に関する講習の受講時期について、消防法令で定められているものは、次のうちどれか",
          choices:[
            {choice:"免状の交付を受けた日以降における最初の４月１日から１年以内、その後、前回の講習を受けた日以降における最初の４月１日から３年以内ごと",answer:false},
            {choice:"免状の交付を受けた日以降における最初の４月１日から２年以内、その後、前回の講習を受けた日以降における最初の４月１日から５年以内ごと",answer:true},
            {choice:"免状の交付を受けた日から３年以内ごと",answer:false},
            {choice:"免状の交付を受けた日から５年以内ごと",answer:false}
          ],
          correct_answer_flg:false, selected:null,
        },
        {
          question:"消防設備士免状の返納について、消防法令上、誤っているものは次のうちどれか",
          choices:[
            {choice:"返納を命ずるのは、消防長又は消防署長である",answer:true},
            {choice:"返納を命ずることができるのは、消防設備士がh相貌法令の規定に違反している場合である",answer:false},
            {choice:"免状の返納命令に従わない場合には、罰則の適用がある",answer:false},
            {choice:"免状の返納命令により、消防設備士の資格を喪失する",answer:false}
          ],
          correct_answer_flg:false, selected:null,
        },
        {
          question:"工事整備対象設備等の工事又は整備に関する講習について次の記述のうち、文中の（　）に当てはまる語句の組み合わせとして、消防法令上正しいものは次のうちどれか。「消防設備士は、（ア）日以降における最初の４月１日から（イ）以内に講習をうけなければならない",
          choices:[
            {choice:"（ア）工事整備対象設備等の工事又は整備に従事することとなった　（イ）２年",answer:false},
            {choice:"（ア）免状の交付を受けた　（イ）５年",answer:false},
            {choice:"（ア）工事整備対象設備等の工事又は整備に従事することとなった　（イ）５年",answer:false},
            {choice:"（ア）免状の交付を受けた　（イ）２年",answer:true}
          ],
          correct_answer_flg:false, selected:null,
        },
        {
          question:"都道府県知事（総務大臣が指定する市町村長その他の機関を含む）が行う工事整備対象設備等の工事又は整備に関する講習について、消防法令上、誤っているものは次のうちどれか",
          choices:[
            {choice:"消防設備士免状の交付を受けた日から5年以内ごとに受講しなければならない",answer:true},
            {choice:"工事整備対象設備等の工事又は整備に従事していない消防設備士もじゅこうしなければならない",answer:false},
            {choice:"消防設備士免状の種類及び指定区分等に応じて行われる",answer:false},
            {choice:"定められた期間内に受講しなければ、消防設備士免状の返納を命ぜられることがある",answer:false}
          ],
          correct_answer_flg:false, selected:null,
        },
        {
          question:"都道府県知事（総務大臣が指定する市町村その他の機関を含む）が行う工事整備対象設備等の工事又は整備に関する講習制度について、消防法令上、正しいものは次のうちどれか",
          choices:[
            {choice:"消防設備士は、その業務に従事することになった日以降における最初の４月１日から５年以内ごとに講習をうけなければならない",answer:false},
            {choice:"消防設備士は、免状の交付を受けた日以降における最初の４月１日から５月１日から２年以内に講習を受け、その後、前回の講習を受けなければならない",answer:false},
            {choice:"消防設備士は、その業務に従事することになった日以降における最初の４月１日から２年以内に講習を受け、その後、前回の講習を受けた日以降における最初の４月１日から５年いないごとに講習をうけなければならない",answer:false},
            {choice:"消防設備士は、免状の交付を受けた日以降における最初の４月１日から２年以内に講習を受け、その後、前回の講習を受けた日以降における最初の４月１日から５年以内ごとに講習を受けなければならない",answer:true}
          ],
          correct_answer_flg:false, selected:null,
        },
        {
          question:"工事整備対象設備等の工事又は整備に関する講習の実施者として、消防法令上正しいものは次のうちどれか",
          choices:[
            {choice:"都道府県知事",answer:true},
            {choice:"総務大臣",answer:false},
            {choice:"消防長又は消防署長",answer:false},
            {choice:"消防丁長官",answer:false}
          ],
          correct_answer_flg:false, selected:null,
        },
        {
          question:"都道府県知事（総務大臣が指定する市町村長その他の機関を含む）が行う工事整備対象設備等の工事又は整備に関する講習の受講時期について、消防法令で定められているものは、次のうちどれか",
          choices:[
            {choice:"免状の交付を受けた日から３年以内ごと",answer:false},
            {choice:"免状の交付を受けた日から５年以内ごと",answer:false},
            {choice:"免状の交付を受けた日から２年以内、その後、前回の講習を受けた日から５年以内ごと",answer:false},
            {choice:"免状の交付を受けた日以降における最初の４月１日から２年以内、その後、前回の講習を受けた日以降における最初の４月１日から５年以内ごと",answer:true}
          ],
          correct_answer_flg:false, selected:null,
        },
        {
          question:"都道府県知事（総務大臣が指定する市町村長その他の機関を含む）が行う工事整備対象設備等の工事又は整備に関する講習の受講時期について、消防法令で定められているものは、次のうちどれか",
          choices:[
            {choice:"免状の交付を受けた日以降における最初の４月１日から１年以内、その後、前回の講習を受けた日以降における最初の４月１日から３年以内ごと",answer:false},
            {choice:"免状の交付を受けた日以降における最初の４月１日から２年以内、その後、前回の講習を受けた日以降における最初の４月１日から５年以内ごと",answer:true},
            {choice:"免状の交付を受けた日から３年以内ごと",answer:false},
            {choice:"免状の交付を受けた日から５年以内ごと",answer:false}
          ],
          correct_answer_flg:false, selected:null,
        },
        {
          question:"消防設備士免状の返納について、消防法令上、誤っているものは次のうちどれか",
          choices:[
            {choice:"返納を命ずるのは、消防長又は消防署長である",answer:true},
            {choice:"返納を命ずることができるのは、消防設備士がh相貌法令の規定に違反している場合である",answer:false},
            {choice:"免状の返納命令に従わない場合には、罰則の適用がある",answer:false},
            {choice:"免状の返納命令により、消防設備士の資格を喪失する",answer:false}
          ],
          correct_answer_flg:false, selected:null,
        },
        {
          question:"工事整備対象設備等の工事又は整備に関する講習について次の記述のうち、文中の（　）に当てはまる語句の組み合わせとして、消防法令上正しいものは次のうちどれか。「消防設備士は、（ア）日以降における最初の４月１日から（イ）以内に講習をうけなければならない",
          choices:[
            {choice:"（ア）工事整備対象設備等の工事又は整備に従事することとなった　（イ）２年",answer:false},
            {choice:"（ア）免状の交付を受けた　（イ）５年",answer:false},
            {choice:"（ア）工事整備対象設備等の工事又は整備に従事することとなった　（イ）５年",answer:false},
            {choice:"（ア）免状の交付を受けた　（イ）２年",answer:true}
          ],
          correct_answer_flg:false, selected:null,
        },
        {
          question:"消防設備士の義務について、消防法令上、誤っているものは次のうちどれか",
          choices:[
            {choice:"消防用設備等が設備等技術基準に違反して設置又は維持されている場合、消防設備士は消防長又は消防署長に届け出なければならない",answer:true},
            {choice:"消防設備士は、その業務に従事する場合、消防設備士免状を携帯していなければならない",answer:false},
            {choice:"消防設備士は、業務を誠実に行い工事対象整備対象設備当の質の向上に努めなければならない",answer:false},
            {choice:"消防設備士は、都道府県知事（総務大臣が指定する市町村長その他の機関を含む）が行う工事整備対象設備等の工事又は整備に関する講習を受けなければならない",answer:false}
          ],
          correct_answer_flg:false, selected:null,
        },
        {
          question:"次の消防法令施行令別表第１に掲げる防火対象物のうち、消防法令上、防火管理対象者を定めなければならないものは次のうちどれか",
          choices:[
            {choice:"診療所で、収容人数が20人のもの",answer:false},
            {choice:"美術館で、収容人数が30人のもの",answer:false},
            {choice:"教会で、収容人数が40人のもの",answer:false},
            {choice:"事務所で、収容人数が50人のもの",answer:true}
          ],
          correct_answer_flg:false, selected:null,
        },
        {
          question:"次の消防法令施行令別表第１に掲げる防火対象物のうち、消防法令上、防火管理対象者を定めなくてもよいものは次のうちどれか",
          choices:[
            {choice:"老人短期入所施設で、収容人数が15人のもの",answer:false},
            {choice:"旅館で、収容人員が30人のもの",answer:false},
            {choice:"カラオケボックスで、収容人員が30人のもの",answer:false},
            {choice:"共同住宅で、収容人数が45人のもの",answer:true}
          ],
          correct_answer_flg:false, selected:null,
        },
        {
          question:"防火管理に関する次の記述の文中の（　）に当てはまる語句の組み合わせとして、消防法令上、正しいものは次のうちどれか「（ア）は消防の用に供する設備、消防用水若しくは消火活動上必要な施設の（イ）及び整備又は火器の使用若しくは取り扱いに関する監督を行うときは、火元責任者その他の防火管理の業務に従事する者に対し、必要な指示を与えなければならない」",
          choices:[
            {choice:"（ア）防火管理者　（イ）工事",answer:false},
            {choice:"（ア）管理について権原を有する者　（イ）工事",answer:false},
            {choice:"（ア）管理について権限を有する者　（イ）点検",answer:false},
            {choice:"（ア）防火管理者　（イ）点検",answer:true}
          ],
          correct_answer_flg:false, selected:null,
        },
        {
          question:"次の管理について権原が分かれている防火対象物のうち、統括防火管理者を定めなければならないものとして、消防法令上、誤っているものはどれか。ただし、防火対象物は、高層建築物（高さ３１ｍを超える建築物）ではないものとする",
          choices:[
            {choice:"地階を除く階数が３の特別養護老人ホームで、収容人員が６０人のもの",answer:false},
            {choice:"地階を除く階数が５の事務所で、収容人員が６０人のもの",answer:true},
            {choice:"２階をカラオケボックスとして使用する地階を除く階数が３の複合用途防火対象物で、収容人数が５０人のもの",answer:false},
            {choice:"地階を除く階数が５の病院で、収容う人員が７０人のもの",answer:false}
          ],
          correct_answer_flg:false, selected:null,
        },
        {
          question:"次のアからウまでの管理について権原が分かれている防火対象物のうち、統括防火管理者をさだめなければならないものとして、消防法令上、正しいものの組み合わせは次のうちどれか。ただし、防火対象物は、高層建築物（高さ３１ｍを超える建築物）ではないものとする　ア：地階を除く階数が５の作業場で、収容人員が８０人のもの　イ：地階を除く階数が４の病院で、収容人数が４０人のもの　ウ：地階を除く階数が３の特別養護老人ホームで、収容人員が２０人のもの",
          choices:[
            {choice:"ア、イのみ",answer:false},
            {choice:"ア、ウのみ",answer:false},
            {choice:"イ、ウのみ",answer:true},
            {choice:"ア、イ、ウすべて",answer:false}
          ],
          correct_answer_flg:false, selected:null,
        },
        {
          question:"消防の用に供する機械器具等の検定に係る表示に関する次の記述のうち、文中の（　）に当てはまる語句として、消防法令上、正しいものは次のうちどれか「検定対象機械器具等は、型式承認を受けたものであり、かつ、（　）の表示が付されているものでなければ、販売の目的で陳列してはならない」",
          choices:[
            {choice:"技術上の規格に適合するものである旨",answer:false},
            {choice:"設備等技術基準に適合するものである旨",answer:false},
            {choice:"型式適合検定に合格したものである旨",answer:true},
            {choice:"性能評価を受けたものである旨",answer:false}
          ],
          correct_answer_flg:false, selected:null,
        },
        {
          question:"消防の用に供する機械器具等の検定について、消防法令上、正しいものは次のうちどれか",
          choices:[
            {choice:"型式承認とは、検定対象機械器具等の型式に係る形状等が総務省令で定める検定対象機械器具等に係る技術上の規格に適合している旨の承認をいう",answer:true},
            {choice:"検定対象機械器具等は、型式承認を受けたものである旨の表示が付されているものであれば、販売の目的で陳列することができる",answer:false},
            {choice:"型式適合検定とは、型式承認を受けていない検定対象機械器具等の形状等が型式に係る形状等に適合しているかどうかについて総務省令で定める方法により行う検定をいう",answer:false},
            {choice:"検定対象機械器具等のうち消防の用に供する機械器具又は設備は、型式承認を受けたものである旨の表示が付されているものであれば、その設置、変更又は修理の請負にかかるものである旨の表示が付されているものであれば、その設置、変更又は修理の請負に係る工事に使用することができる",answer:false}
          ],
          correct_answer_flg:false, selected:null,
        },
/*

        {
          question:"",
          choices:[
            {choice:"",answer:false},
            {choice:"",answer:false},
            {choice:"",answer:false},
            {choice:"",answer:false}
          ],
          correct_answer_flg:false, selected:null,
        },
*/
      ]);

        console.log(tests.length);
        for (let i = tests.length - 1; i >= 0; i--) {
          for (let j = tests[i].choices.length - 1; j >= 0; j--) {
            let r = Math.floor(Math.random() * (j + 1))
            let tmp = tests[i].choices[j]
            tests[i].choices[j] = tests[i].choices[r]
            tests[i].choices[r] = tmp
          }
        }
        for (let i = tests.length - 1; i >= 0; i--) {
          let r = Math.floor(Math.random() * (i + 1))
          let tmp = tests[i]
          tests[i] = tests[r]
          tests[r] = tmp
        }
      return {
        tests,
      }
    }
  }
</script>