# Bertalign
This repository is forked from the bfsujason/bertalign repo.

I made following changes.

(1) The original code use google_tran model to detect text language, but google_tran is no longer available. Therefore I use unicode value to detect whether the text is Chinese or not.
(2) Change the default model to BAAI/bge-m3.
(3) Update the requirements.txt.
(4) Make some minor adjustments.

The original repo run on linux. For windows users, choose faiss-cpu instead of faiss-gpu-cu12 in requirements.txt. 

## Installation

Please see [requirements.txt](./requirements.txt) for installation. 

### You can also install Bertalign and run the examples directly in a [Google Colab notebook](https://colab.research.google.com/drive/123GhXwgwmQp1F5SVZ74_uIgyxo6hLRq0?usp=sharing).

## Basic example

Just import *Bertalign* and initialize it with the source and target text, which will detect the source and target language automatically and split both texts into sentences. Then invoke the method *align_sents()*  to align sentences and print out the result with *print_sents()*.

```python
from bertalign import Bertalign
```

```python
src = """从甲午中日战争到戊戌维新前后,中国民间舆论关于既存中国学术“无用”的观念相当流行;这一观念显然影响了朝廷的决策,对华北义和团的借重提示着朝廷基本接受了中学之上层正统已不足以救亡图存,故走向基层,启用中国传统中任何可以尝试的资源,也就是往异端方面寻求力量和支持。
虽然启用“怪力乱神”的举措并未得到多数士人的认可,却实际促成了一种以边缘上升为表征的“异端正统化”进程。
这一转变上承太平天国运动,下及新文化运动,其影响之余波至今犹存,而最具象征性的转折点就是庚子义和团事件。
其间一个重要因素是作为异端进入中国的西潮无形中对昔日中国边缘文化的支持,若非西潮冲击迫使无力退虏送穷的既存主流文化退居二线,原来的本土异端便难以上升为正统。
本文试将义和团事件置于这一历史转变的进程中进行考察,并藉此分析传统文化中属于“子不语”的怪力乱神怎样以一种诡论性的( paradoxical)方式从异端走入正统。
1.思想的竞争者与社会分野的盟友
张之洞在戊戌(约1898)年指出,中国人反教,大抵“学士倡之,愚民和之,莠民乘之,会匪游兵藉端攘夺,无故肇衅”。
章太炎对此大致同意,他从文化历史渊源探讨近代中国何以排教及怎样排教,区分民众、士人与政府三方面,所论相当深入。
太炎以为,中国百姓本不排外教,“海外诸教,释氏先入于汉世矣,天方继入于唐世矣,基督晚入于明世矣。
是时人民望此以为导师,欢喜踊跃,如大旱之见长蝀;特一二士人以其背弃儒法,而被以异端之名,非社会之总意然也”。
惟近代确实“常有排教之事”,则又因“基督教之来也,常挟国权以俱来,而所至有陵轹细民之事;入其教者又藉此以武断闾里之间,是所以促其反动”。
中国传统社会固然“敬宗而严父”,但“佛教之入也,亦曰六亲不敬、鬼神不礼,而未闻传其教者之被菹醢利玛窦南怀仁辈以基督旧教传播中国且二百年,自海衅未启以前,谁以罗马教宗为悖德忘本而反抗之者?若夫韩愈、杨光先辈,以其私意,抒之简毕、陈之庙堂,则于全体固无所与”。
对杨光先的不欣赏大致是主张“学术开放”的国粹学派之共识,刘师培也指责“杨光先诋西书为诞肆,乃直声既著于明廷,仕籍复标于清史。
彼斤斤于学术之间衡量口夷]夏,而出处大节转舍夏就口[夷]”。
太炎申论说,若“政府之排教”,则“其意本不在异种异教,而惟集众倡乱之为惧”。
正因“以其集众倡乱而排之,则不必于异种之教然也,虽同种之白莲、闻香亦然;不必于破坏宗法之教然也,虽儒流之党锢、道学亦然。
是故政府之排教也以其合群而生变;人民之排教也,以其藉权而侮民”;皆与“真基督教”的价值观念无大关系。
士人中“今日亦有以彼教为无君父而视之如洪水猛兽者矣,然人民之偾起排教者,其意乃绝不在是。
浸假而基督教人之在中国循法蹈义、动无逾轨,则人民固不以异教而排斥之,亦不以异种而排斥之;其相遇也,与昔之天竺法师无异。
虽以百千士人著书攻击,犹往日宋儒之辟佛而已,而人民不因是以起其敌忾之心也”。
这是迄今为止关于近代中国排教最为言简意赅的论述,政府和一般人民之排教主要均由于实际利益的冲突,而士人则更加注意其文化层面的冲击,且主要还不仅是视其为“外教”,而是更重视其异端性质中隐含的威胁,即可能颠覆中国的传统伦理。
这里当然还有差异,比如,戊戌之前以排外和反教著称的湖南,由于当地几乎没有定居的传教士,教民数量不多,其反洋教活动以基于传闻的想象为主,体现出一种强烈的防患于未然的文化忧患意识,故特别注重中西文化竞争。
但在传教事业相对成功而教民众多的地区,士人的观感可能就相当不同。
据宋恕在庚子后的观察:“基督教来禹域,士大夫憎之甚,鲜肯虚心阅其语录”。 故“今禹域之入基督教籍者,其大多数不出二种:甲种为极可怜之人,乙种为极可恶之人。
甲种良懦之人,被逼于贪酷官吏,不得已而求保护其性命财产于西洋宣教师。
乙种诈毒之人,入籍之原因,欲假西洋宣教师之势力以驱使官吏而鱼肉乡里。 庚子义和团之变实由于乙种所激成,而甲种亦牵连而得惨祸。”
庚子以后,“官畏西人愈甚,因之畏基督教信徒亦愈甚”；更由于“偿外国费之故,剥削民生亦愈甚;因之甲种、乙种入籍之人皆有日多一日之现象”。
盖“一入基督教则可以免于无厌之赋税、非法之刑戮彼入者固亦大半属于可怜者矣,然其属于可恨者亦居少半焉”。 这两类入教者“皆不得认为真基督教之信徒”。
江苏江宁县文生徐堃锡所看到的情形稍异,他发现“自天主耶稣两教流入中国,其教堂由省会而郡县而乡镇,无地无之。
早年入教者万中之一,近年入教者千中之一;早年入教者非愚民即奸民,近年入教者奸民半良民亦半”。
徐氏感觉“尤堪痛恨者”,是“士夫中亦渐有信之者,而间有入之者”。
这是一个不小的变化,自清初那次所谓“礼仪之争”后,读书人向视西教为异端,故李鸿章在1880年曾告诉李提摩太:许多乡民固然因物质原因皈依基督教,士人中却无一信教者。
此话虽未免失之过偏,大体应符合当时的情形。 不过八九年后,就出现这样的转变,的确使关注中西学战的“有心人太息深之”。
而徐氏观察到的入教原因却与宋恕所见一样,即“无论何等人一入教,地方官即不敢过问,且可与之分庭抗礼。
奸民藉入教以作威福,良民藉入教以保身家”。
章太炎也注意到类似的现象,他认为:“中国人的信仰基督,并不是崇拜上帝,实是崇拜西帝。
最上一流，是借此学些英文法文,可以自命不凡;其次就是饥寒无告,要借此混日子的;最下是凭仗教会的势力去鱼肉乡愚、陵轹同类。
所以中国的基督教,总是伪基督教,并没有真基督教。”
这里借入教学外语的“最上一流”,或即徐堃锡眼中转向基督教的“士夫”。
在太炎看来,不论上流下流,这些人信教入教的出发点均是社会的而非思想的。
可知章太炎并不一定反对“真基督教”的教义或思想,而宋恕甚至还相当赞许基督教。
在宋恕1902年为瑞安演说会起草的《章程》中,曾列有几条“禁演律”,其中就包括“不许盲贬孔教、佛教(道德一线全恃孔教、佛教绵延,岂可盲贬);不许盲贬基督教(基督教经虽多不合哲学、科学之处,然其提倡博爱主义,实亦西洋道德一线之所系也)”。
这里主要注重的是作为意识形态的基督教在西方的社会功能,到1903年他进而认为,“儒教及基督教最为相近,而其理想皆不如佛教之高。
佛教虽高,而易入于空而不实、泛而不切之境。
故必须融为一冶,而后此世界能放大异彩,人类之幸福能进”。
基督之主义乃主张社会主义,而中国“孔孟之主义,本亦近于彼土所谓社会主义”,两者是相通的。
若“唐、宋时信孔孟之主义者居十之二三,则立宪共和之政治必早出于茫茫九州,何尚有女真、蒙古之祸之悲哉”!今日中国“苟基督信徒如春水之骤涨,则亦可望其拯生民于涂炭。
乃观所谓日多一日之基督信徒者,大都非恕之所谓基督信徒也”。
不论宋恕对基督教义的理解是否准确,至少像他和章太炎这样的士人并不一定反对甚或相对赞成“真基督教”的教义或思想。
但基督教在中国的社会功能不仅不像其在西方那样为“道德一线之所系”,反成为可以“鱼肉乡愚、陵轹同类”的凭藉;许多中国人入教固是为了寻求保护以抵制贪酷官吏的压榨,同时也有不少“教民”恐怕更看重并利用教会那带进攻性的一面。
这些行为,特别是后者,导致了基督教在华的“伪化”,从而在很大程度上引起了朝野的“排教”。
庚子义和团事件可以被视为晚清“教案”的一个高潮,其最显著的特点是民间的“反洋教”运动得到朝廷的支持,是近代整体中西竞争的一个组成部分,具体又落实在“教民”和“拳民”这两大社会群体的冲突和竞争之上。
不过,西方传教士向来不仅视中国任何带宗教意味的社会组织为竞争对手,同时又主动承担起以(西方)“科学”反对(中国)“迷信”的任务;后者通常被视为“神拳”的一个重要侧面,故在传教士看来,义和拳这一“神拳”在思想观念上是基督教的双重竞争对手。
另一方面,对那时多数中国士人(以及相当数量的民众)而言,基督教和神拳大致都属于“子不语”的“怪力乱神”范畴,其社会分野是接近的;这不仅反映在士人对两者都不认可,同时也可从不少民间反叛者常寻求传教士为造反的政治盟友这一点看出。
由于传教士最终关怀的是天国,他们对中国民间宗教极为重视。
不论信何种教,信教者总是比不信教者更关心彼世。
许多传教或将中国各宗教信仰视为竞争对手,或将其视为潜在的合作者,来华新教传教士先驱者之一的郭士立Charles Gutzlaff 1803——1851)即视龙王为中国人崇拜的象征,因而也是基督的主要竞争对手。
他曾衷心希望,而且确信,总有一天“龙王会被褫夺王冠,而基督则被尊为全中国唯一之王和崇拜的唯一对象”。
其他一些传教士则注意阅读佛教道教文献,如李提摩太( Timothy Richard,1845-1919)即曾下大力研读一些佛教道教经书,希望能借此帮助他与中国士人的沟通。
但在那时,懂得一些佛道教知识大概多能有助于与大众的交往;而对于多数正统儒士来说,恐怕适得其反。
另一方面,类似林乐知( Young. Allen1836-1907)、李提摩太这样的传教士则长期在中国通过演示化学和电学实验等提倡“科学”。 他们的主要目的当然是希望借西来的科学证明西方文化的优越,从而使中国人尊信上帝(在传教士眼中的上帝本应是普世性的,其这一做法实际等于承认“上帝”的西方区域性);但不知是否无意中受到科学的影响,他们同时自动承担起在中国反对迷信的社会角色。
正如林乐知本人所说,他希望借助这些实验说服中国人,使其知道他们“许多迷信思想的愚蠢和谬误”。
虽然他将科学用来支持基督教教义的努力基本未能成功,在向中国学生表演煤气点灯时却能成功地使他们“目瞪口呆”。
李提摩太也一直试图使中国官员和士人对“科学的奇迹”产生兴趣,他从1881年到1883年坚持每月向中国士大夫演讲各式各样的“奇迹”,而其用以形容其听众观众反应的最常用字眼是“震惊”。
李氏发现,中国士大夫觉得“近代科学的魔力远超过所有其他魔法”。
林乐知其实知道,相信宗教奇迹的时代已过去了。 但他确信,在中国,“如果将科学有技巧地演示出来”,则其功用几乎可像宗教奇迹一样“奇妙而战无不胜”。
这一见解揭示了科学在当时中国传教界恰扮演着“宗教奇迹”在西方的社会角色。
正是因为这些科学演示充满了奇迹、魔力、震惊和目瞪口呆一类效果,传教士自己无意中认同于江湖艺人和风水先生一流。
早年对传教士比较正面的称呼,大约就是“讲古鬼”。
许多人将传教活动视为类同民间艺人的“讲古”(约即今日的“说书”),而洋人本来又被视为“番鬼”,所以实连江湖艺人都不如。
尽管中国士人实际上多少都相信一些风水,但风水先生作为一个社群的社会地位并不比江湖艺人高。
具有讽刺意味的是,李提摩太自认他向中国人传播科学的目的之一就是消除他们对风水的迷信,他本人却曾被中国人请去看过风水,这个例子说明确有中国人将传教士视为风水先生一流。
故传教士自身这类举动不啻自居异端,实际上强化了士人和民众在社会分野上轻视传教士的认知。
与士人相反,民间反抗朝廷者则常常认同于传教士或将传教士视为盟友。
早在1834年,福建一个企图起事者就向美国传教士雅稗理( David Abeel 1804-1846)建议联合造反。
最明显的例证当然还是太平天国以其简化改造的基督教为正式的意识形态,建国后更确立“拜上帝教”为官方宗教。
这些造反者不用白莲教、八卦教一类民间既存宗教形式,而偏偏选中外来的基督教,即使是出于偶然,也揭示了中国社会某种思想权势转移。
过去不少研究认为那时士人支持清廷反对太平天国,是基于对外来的基督教教义感觉很大的威胁,其实当时基督教在华地位尚低,基本与民间“邪教”相类似,故士人虽然多从文化上考虑问题,但基本上是将其作为反名教的“怪力乱神”看待。
换言之,在中西与文野两大对应关系中,多数士人是从文野角度考虑问题。
在一定程度上,可以说太平天国体现了中西“怪力乱神”因素的结合。
在镇压太平天国叛乱方面朝廷与士人结成了同盟,但双方的出发点相当不同,朝廷恐怕主要视为统治权的争夺,而士人更多看到文化异端向正统的挑战。
这里还掺杂着一个更复杂的因素,即清初和清季都得到凸显的满汉关系。
过去研究太平天国者对此或不甚注重,或过多强调。
实际上,满清虽是外族入主,但由于华夏政治制度及纲常名教对维护其统治有利,清廷在汉人中消弭满汉之分的努力也相当成功。
清初之治,确有胜过明季之处。
满人接受华夏文化的实际程度,超过元代蒙古人;满汉两族在政治待遇上的差别,也不如元代蒙人与汉人间的差别大。
凡此种种,都不同程度地减低了汉人对满族统治的嫉恶。
到西潮东渐后,在乾嘉时极为忌讳的词汇“夷狄”,到咸同时略经踌躇后即为汉族士人广泛使用;清廷不以为忤,而士人亦不再觉有自我检束的必要,足见多数时人早已不视清为夷狄。
这一切都表明清虽是外族入主,中国却并未达到顾炎武所谓“亡天下”的地步,这正是汉族士大夫助清廷剿灭太平天国的文化基础。
当太平军以反满民族意识和外来之拜上帝教为号召起兵造反时,绝大多数食毛践土的士人乃能站在清廷一边,捍卫已为中夏之主的满清政权。
其根本原因,就是因为太平天国讲的正是“子不语”的怪力乱神,代表一种“亡天下”的可能。
许多汉族士人并非不为反满民族意识所动,但“亡天下”的危机感显然压倒了这相对狭义的民族意识。
司马迁已注意到,秦末陈涉不过一“至微贱”的匹夫起事,“然而缙绅先生者徒,负孔子礼器往,委质为臣者,何也?以秦焚其业,积怨深而发愤于陈王也”。
蒙文通先生据此指出,“盖宗社之怨既深,种族风教殊,而道术之痛尤笃也”。
汉人的缙绅先生者徒能起而助清廷剿灭太平天国,即因宗社之怨虽在种族风俗亦殊,但教与道术尚存,有妥协之余地而洪杨正所谓“怪力乱神”者也。
在太平天国之后,中西“怪力乱神”因素的结合仍在持续,山东一伙起事者即曾要求李提摩太作他们的首领。
英国驻马尾领事法磊斯( Sir Everard D.H. Fraser)在1898年告诉莫理循(George.E.Morrison)说:来自广州的英国情报显示,“法国人已经铺平了吞并广东和广西两省的道路。 法国人通过在他们的传教士保护下皈依法国教会的‘教民们’建立了一个国中之国,可以在法国人认为合适的任何时机发动一起到三起地方叛乱。
他们接受任何流氓无赖皈依他们的教会,强使整村整村的人入教,公开滋扰邻居和对抗当局。”
周锡瑞( Joseph W. Esherick)关于义和团运动起源一书更详细揭示了19世纪末山东起事者与传教士的频繁接触。
具有诡论意味的是,高树的《金銮琐记》说:刑部尚书赵舒翘,为刚毅所保荐,受刚命往涿州“查视团匪,密约入京”。
不久“团匪亦蜂拥至,日以焚杀为事。
城外良民老幼男女将近百人,团匪诬以白莲教,杀之于菜市。
舒翘不救,但言劫数而已”。
按“团匪”何不径呼其欲杀者为洋教?若此记载属实,则“团匪”眼中所见,正其同类竞争者之一的白莲教;倘不实,则说明记录的士人把自己视洋教与白莲教类同的认知投射到拳民身上,仍具提示性。
实际上,张穆早在道光二十四年(约1844)时即已在驳斥那种认为“天主教与白莲教等”的观念,强调二者有根本的区别,说明类似观念渊源甚早。
合上述事实而综观之,许多人把基督教视为类似白莲教、八卦教一类的异端大致是无问题的。
这样,尽管有条约的保护,传教士与中国士人的交往直到19、20世纪之交始终有限。
合前引李鸿章、宋恕、徐堃锡、章太炎等人的观察而共论,梁启超在庚子后数年所说“耶教之入我国数百年矣,而上流人士从之者稀”一语大体可立。
这当然既受中西文化竞争的影响,也有中国“教民”利用基督教在华特殊社会功能所起的作用,但太平天国事件已充分表明,在中西与文野两大对应关系中,士人实更注重后者。
。"""

tgt = """Between the Sino-Japanese War [in 1894–95] and the Hundred Days' Reforms [in 1898], public opinion said Chinese scholarship was ‘useless'—an opinion that profoundly affected Court thinking. The Throne's ultimate decision to rely on the Boxers in North China implied that it accepted the opinion that significant elements of orthodox (zhengtong 正统) thought were incapable of saving the empire and forced it to begin sifting through Chinese tradition for other resources.1 Ultimately, the Court sought strength and support from heterodoxy (yiduan 异端).
Although a majority of the educated elite disagreed with adopting the methods of ‘strange things, feats of strength, disorder, and spiritual beings' (guai li luan shen 怪力乱神) (i.e. the strange and supernatural), the Court's decision brought about a process that would raise the marginal through a process of ‘orthodoxizing the heterodox.'2
This transformative process began during the Taiping Rebellion [1850–1864] and ended in the New Culture Movement [1915–1919], but its impact continues to be felt today. The Boxer Incident represents the most symbolic moment within this process.
The Western tide, entering China as heterodoxy, would ultimately provide the support necessary for making marginal Chinese cultures orthodox. If the impact of the Western tide had not forced mainstream culture to recede, because it was unable to fend off invaders and alleviate poverty, it would have been difficult for indigenous heterodoxies to rise to the status of orthodoxy.
This chapter is an examination of the Boxer Incident within the context of this long process of historical change that explains the paradoxical manner in which ‘the strange and supernatural' that belonged to ‘what Confucius does not talk about' (Zi bu yu 子不语) transitioned from heterodoxy to orthodoxy.
Intellectual Competitors and Allies in Social Categorization
In 1898, Zhang Zhidong 张之洞 (1837–1909) argued that most Chinese opposed religion: “scholars argue against it, foolish people join it, bad subjects take advantage of it, and secret societies, bandits, and roaming soldiers use it to cause trouble."
In general agreement, Zhang Taiyan offered a penetrating analysis of the cultural and historical reasons why modern Chinese commoners, scholars, and the state resisted religion.
Zhang argued that the Chinese masses were not initially resistant to foreign religions: Among the overseas religions, Buddhism came first during the Han dynasty, Islam followed in the Tang, and Christianity in the late Ming.
Contemporaries looked up to them like jubilant peasants whose crops grow in times of severe drought. A few scholars considered them heterodox because they departed from the Way of Confucius, but this view did not represent the broader feeling in society...
[Only in recent times] have there been incidents of resistance to the religion [because] missionaries with the support of the foreign powers cause trouble and oppress the common people. Chinese Christians use their religion to coerce their neighbors, which is the real reason for the reaction against Christianity.3
Although Chinese traditional society “respected the ancestors and revered the father," Zhang argued, when Buddhists arrived, it was claimed that Buddhism showed no respect for relatives or ancestral spirits, but no one heard that the Buddhists were picked apart and minced into stew meat. Matteo Ricci and Ferdinand Verbiest, as well as other Jesuits, proselytized Christianity for close on two hundred years. Before the naval dispute, who would have regarded the Vatican as immoral or ungracious and fought against it? [The anti-Buddhist] Han Yu 韩愈 (768–824) and [anti-Christian] Yang Guangxian 杨光先 (1597–1669), as well as others, expressed their private opinions in books and at the Court, but did not contribute anything to the entire picture.
Disagreement with Yang Guangxian was common among the proponents of national essence who advocated ‘intellectual openness.' Liu Shipei criticized Yang for “defaming Western books as absurd and directing his voice to the Ming Court, which continued to reverberate in Qing times.
He trifled with scholarship in his comparison of the barbarian with the Chinese, but adopted barbarian methods on important issues."
4 Zhang Taiyan argued, if “the government opposed religion," then “it was not because it was a heterodox, but because the government feared people gathering together might lead to chaos."
Zhang continued, [because] the opposition to religion concerned its mob tendencies and not its heterodox origins, it was the same [objection] to the indigenous White Lotus cult and the Teachings of Incense Smelling (wen xiang 闻香); the government did not object to religion because it destroyed the patriarchal clan system, but for the same reasons it objected to Daoxue (道学) factions among Confucians. The government's opposition to religion was ultimately based on the fear that when religious people gathered together something untoward might occur.
The people, however, opposed religion because it was used to oppress them. These oppositions had little to do with the value system of “real Christianity."
Among the scholars, “there were those who saw Christianity as extremely dangerous because Christians did not venerate the Emperor or the father figure, but the people's rejection of Christianity had nothing to do with this perspective.
If Christians are well behaved in China, the people will not reject the religion because it is barbarian; the encounters will be no different than with Indian [Buddhist] monks in the past.
Although thousands attack Christianity in their writings, it is like the repudiation of Buddhism by Song Confucians. The people will not be antagonistic to Christianity because of the scholars."
5 This is the most concise argument about the opposition to religion in modern China—the government and common people rejected religion because of clashes over practical interests, but scholars focused on its threats on a cultural level. The scholars saw Christianity as a threat not merely because it was a “foreign religion," but because its heterodox nature might undermine traditional Chinese ethics.
There were additional differences. In Hunan, famous for being anti-foreign and antireligious prior to 1898, the opposition to foreign religion was based on rumors and imagination because there were almost no missionaries there and very few Christians.6
In areas where proselytization was relatively successful, and Christians were found in numbers, the perspectives and opinions of local scholars were considerably different.
As Song Shu observed after 1900, When Christianity arrived in China, scholars hated it and were rarely willing to read its works [so] there were only two types of Chinese who converted to Christianity: the very pitiable and the very detestable.
The pitiable were kind and weak, they were bullied by corrupt and cruel officials and turned to Western missionaries for protection.
The second type were bullies who converted to Christianity to use the power of Western missionaries to boss around officials and harass other villagers—this second type caused the Boxer Incident of 1900, but the first type also suffered greatly because of them.
[After 1900,] officials were even more afraid of Westerners and therefore even more afraid of [Chinese] Christians... [Later,] because of the Boxer Indemnity, the government began exploiting the commoners to an even greater extent resulting in the growth of both types of converts.7
Once converted, a Christian is exempted from endless taxes and illegal persecution. The majority of these Christians are pitiable and the minority are detestable [but both types of converts] should not be considered true Christians.8
In Jiangning County, Jiangsu, Xu Kunxi 徐堃锡 observed a slightly different situation. He found, ever since Catholics and Protestants entered China, their churches have spread everywhere to capitals, county seats, and villages.
In the early years, only one in ten thousand converted to Christianity, but in more recent years it is one in a thousand. In the early years, either foolish or treacherous people converted, but in recent years about half the converts are wicked and the other half good.
Xu felt “it is disgusting that some scholars believe in Christianity and occasionally convert."
Xu was noticing a significant change. After the “Rites Controversy" in the early Qing, scholars began to view Western religion as heterodox.9 In 1880, Li Hongzhang 李鸿章 (1823–1901) told Timothy Richard (1845–1919) that many villagers converted to Christianity for material reasons, but that scholars did not believe in it.
Li's comment was generally right, but within eight or nine years there was such a dramatic change that those who paid attention to the intellectual war between China and the West truly wondered at it.
What Xu saw as the primary reason for converting to Christianity was the same as Song Shu—“no matter which class a Christian convert came from, the local officials dare not interrogate him. Instead, he is in a position to challenge them.
The wicked convert to Christianity to bully others while the good do so to protect themselves and their families."
10 Zhang Taiyan also noticed a similar phenomenon. He thought, Chinese who believe in Christ are not worshipping God, they are worshipping the West.
The highest ranking [converts] try to learn some English and French to exalt themselves, second are those who are cold, hungry, and unemployed who depended on the religion to make their living, and the lowest use the influence of the churches to bully villagers and their neighbors.
Therefore, Chinese Christianity is fake Christianity; there is no true Christianity in China.11

For Zhang Taiyan, both the upper and lower ranks joined churches for social, but not intellectual reasons.
Zhang Taiyan did not necessarily oppose the doctrines or ideas of “true Christianity" and Song Shu even approved of them.
In 1902, Song Shu drafted rules for the Rui'an Debate Society. In the section “Forbidden Speech," he included “blind denigration of Confucianism and Buddhism (morality is based on Confucianism and Buddhism, how can they be blindly denigrated?). Blind denigration of Christianity is also forbidden (although the Bible has many unreasonable and unscientific passages, Western morality is based on the Christian doctrine of universal life)."
Song focused primarily on Christianity's social function in the West as a form of ideology. In 1903, Song extended his thoughts, “Confucianism and Christianity are quite similar, but neither are as lofty as Buddhism in their ideals.
Although the ideals of Buddhism are high, it is easy to slip into emptiness and unreality.
The three religions must be combined for the world to be glorious and human happiness to increase."
The doctrines of Christianity advocate communalism (shehuizhuyi 社会主义) and “the doctrines of Confucius and Mencius were originally quite close to what other countries refer to as communalism." The two are interconnected.
If “in Tang and Song times, as much as twenty or thirty percent believed in the doctrines of Confucius and Mencius, then the politics of a constitution and a constitutional republic would have appeared early in the Nine Prefectures [China]. We would have avoided such tragedies as the calamities brought about by the Ruzhen and Mongols! If today in China, “the number of Christians dramatically increases, the people might be saved from utter misery.
Although there are more and more socalled ‘Christians' every day, they are not what I would call Christians."
12 Whether or not their understanding of Christian doctrines was correct, Song Shu, Zhang Taiyan, and other scholars did not oppose, and even seemed to approve of, the doctrines of ‘real Christianity.'
In China, however, Christianity was not being used for its ‘morality' as in the West, but as a tool for “bullying villagers and neighbors." Many Chinese did join churches seeking protection from corrupt officials while others took advantage of the aggressive aspects of the churches.
These practices, particularly the latter, led to the ‘falsification' of Christianity in China and, to a great degree, the ‘anti-religiosity' among the Court and Country.13
The Boxer Incident can be seen as the climax of the ‘case concerning religion' in the late Qing. The most distinctive feature of the Boxer Incident was the Court's decision to support a folk-based ‘anti-Western religious' movement, which made the Boxer Incident part of the broader struggle between China and the West; specifically, the struggle between two social groups: the ‘Christians' and the ‘Boxers.'
Western missionaries, however, not only looked at other religiously-inspired social organizations in China as their competitors, but they also believed it was their duty to use (Western) ‘science' to oppose (Chinese) ‘superstition.' Missionaries looked at ‘spiritual boxing' as an important example of superstition. For the missionaries, then, the Boxers as ‘spiritual warriors' posed a dual intellectual challenge to Christianity.
For most scholars (and many of the common people), however, both Christianity and the Boxers belonged to the category of ‘the strange and supernatural' that ‘Confucius does not talk about' and therefore shared social boundaries. The similarities between Christianity and spiritual boxing cannot only be seen in the scholarly resistance to both, but also in the political alliances folk religious leaders sought with Christian missionaries.14
The missionary concern with Heaven meant they paid particular attention to Chinese folk religions.
No matter what religion they believe in, believers are always more concerned with the afterlife than nonbelievers.
Christian missionaries either viewed Chinese religious believers as their competitors or potential allies. Charles Gützlaff (1803–1851), one of the earliest Protestant missionaries, understood the Dragon King (longwang 龙王) as the symbol of Chinese worship and the primary competitor to Christ.
Gützlaff sincerely hoped and believed that one day “the dragon being dethroned, Christ will be the sole king and object of adoration throughout this extensive empire."
15 Other missionaries, however, devoted themselves to reading Buddhist and Daoist scriptures. Timothy Richard, for example, intensely studied Buddhist and Daoist texts in the hopes of facilitating his conversations with Chinese scholars.
Some knowledge of Buddhism and Daoism probably helped Richard communicate with common people, but such knowledge would have harmed the reputation of most orthodox Confucians.16
Missionaries such as Young John Allen (1836–1907) and Timothy Richard performed chemical and electrical experiments to promote ‘science' to demonstrate the superiority of Western culture and convince Chinese to worship God (God, in the missionaries' eyes, was universal, but in their methods they admitted the Western territorial characteristics of ‘God'). Although it is not clear, Allen and Richard probably understood the influence scientific ideas had in supporting their social role in fighting against superstitions in China.
Allen hoped his scientific experiments would convince Chinese of the “follies and mistakes of many superstitious ideas."
Although Allen generally failed in his attempts to use science to support Christian doctrines, his lighting of gas in front of his Chinese students “dumbfounded" them.
Richard tried to interest Chinese officials and scholars in “scientific miracles." From 1881 to 1883, he gave monthly lectures and performed all manner of “miracles" for Chinese scholars and frequently used the word “shocked" to describe his audience's reaction.17
Richard discovered that Chinese scholars felt “the magic of modern science far surpassed all other magic."
18 Allen knew the era of magic had passed, but firmly believed “if science is skillfully performed" in China, it could almost be as “wondrous and unassailable" as religious miracles.19
Allen's opinion illustrates that in China missionaries performed the social role of ‘miracle workers' in the West.
Because his scientific experiments were miraculous, magical, and shocking, missionaries inadvertently equated themselves with folk entertainers and fengshui masters.
In the early years, a more positive term for missionaries was “demon fabulists" (?jianggu gui 讲古鬼).20
Since many people viewed missionary activities as similar to folk artists, ‘fabulists' (similar to today's ‘storytellers') and foreigners were both known as ‘exotic ghosts'; they were considered inferior to itinerant folk entertainers.
Although Chinese scholars more or less believed in geomancy, they considered fengshui masters as a social group even lower than popular entertainers.
Ironically, one of Richard's goals in promoting science was to eliminate the superstition of geomancy. Richard himself, however, was once asked by Chinese to be a geomancer for them, which suggests that Chinese perceived missionaries as fengshui masters.
Missionaries not only positioned themselves as heterodox through their practices, but they also inadvertently strengthened the perception by scholars and the people that they were part of an inferior social group.
In contrast to scholars, leaders of popular rebellions against the dynasty often identified with missionaries or viewed them as allies.
As early as 1834, a rebel leader in Fujian proposed an alliance with American missionary David Abeel (1804–1846).21
The most obvious example of this kind of alliance is, of course, the Taiping rebels, who adopted a simplified version of Christianity as their formal ideology and established “the Religion of God-Worshippers" as their official religion after founding their state.
That the Taipings did not use preexisting folk religious sects such as White Lotus or Eight Trigrams as their inspiration, but chose an imported Christianity, illustrates a certain shift of intellectual power in Chinese society.
Many historians have argued that the scholars supported the Qing Court and opposed the Kingdom of Heavenly Peace because they were threatened by foreign religious doctrines, but even before the Taiping Rebellion, Christianity was already considered to be as low as a folk ‘heretical sect.' Although most Chinese scholars viewed Christianity through a cultural lens, they viewed it as something ‘strange and supernatural' that opposed orthodoxy.
In other words, between the two major diametrical relationships of China/West and civilized/barbarian most scholars saw the relationship of Christianity to the Taiping Rebellion through the dichotomy of civilized/barbarian rather than China/West.
The Taiping Rebellion represented a combination of Sino-Western supernaturalism.
To defeat the Taiping rebels, the Court allied itself with scholars, though their motivations were completely different. The Court viewed the Kingdom of Heavenly Peace as a rival for power while scholars saw it as a cultural heterodoxy challenging the orthodox.
A further complicating factor was the evolving relationship between the Manchus and Han in the Qing, which previous historians have overlooked.

Although the Manchus were of a different ethnicity, they adopted the Chinese political system and ethical orthodoxy to strengthen their control over the empire. Their efforts to reduce the differences between Manchu and Han were quite successful.
Early Qing rule was indeed better than that in the late Ming.
Manchus integrated Han culture into their own far more effectively than the Mongols in the Yuan. Also, the difference in political status between the Manchus and Han in the Qing was less than that between the Mongols and Han in the Yuan.
All of these factors lowered Han animosity towards Manchu rule.
When the Western tide spread to the East, Han scholars often described Westerners with the phrase ‘barbarian tribe' (yidi 夷狄), which had been considered a taboo anti-Manchu word during the Qianlong and Jiaqing reigns. By the late Qing, however, the Court was no longer offended by the term and scholars stopped restraining themselves, which indicates that many contemporaries had ceased viewing the Manchus as a barbarian tribe.22
All of this illustrates that although an ethnic minority ruled the Qing, China had not yet reached the stage that Gu Yanwu 顾炎武 (1613–1682) called “the loss of All Under Heaven," which was the cultural reason why Han scholars allied themselves with the Qing Court against the Kingdom of Heavenly Peace.
When the Taiping army used a combination of anti-Manchu racialism and a foreign-God-worshipping religion as their call to arms, many loyalists stood side-by-side with the Qing Court to protect Manchu Qing political power because the Manchus were defending the core values of the Han.
The fundamental reason for the scholarly opposition to the Taipings was that the rebels stood for the ‘strange and supernatural' and represented the possibility that ‘All Under Heaven' would be lost.
This is not to say that Han scholars were not moved by anti-Manchu racialism, but that the sense of crisis of losing ‘All Under Heaven' outweighed a narrowly defined racial consciousness.
Sima Qian had said that at the end of the Qin, Chen She led “a motley band" of border guards in revolt. “Later, gentlemen and scholars did not hesitate to take up the ritual vessels of Confucius and journey to Chen's side, where they presented gifts and begged to become his ministers. Why was this? Because they were incensed at the Qin dynasty for having burned their books and interrupted their labors, and they hoped that King Chen would help them vent their rage and accomplish their revenge."
Meng Wentong 蒙文通 (1894–1968) took this sentiment a step further, “Although resentment for other clans is deep, and the cultures of countries and races are different, the greatest danger is the loss of orthodox values."
23 Despite the resentment over differences in race and culture, Han gentry rose to help the Qing Court exterminate the Taiping Rebellion because there was room for compromise as long as learning and orthodox doctrines still existed. [Taiping leaders] Hong Xiuquan (1814–1864) and Yang Xiuqing (1821–1856), however, were representatives of ‘the strange and supernatural.'
After the Taiping Rebellion, the combination of Chinese and Western ‘strange and supernatural' elements continued to be significant. In Shandong, a group of rebels demanded Richards become their leader.24
In 1898, Sir Everard D.H. Fraser, the British Consul-General at Mawei, told George E. Morrison that British secret intelligence revealed: “the French through their missionaries, whose protection of their ‘converts' sets up an imperium in imperio, have paved the way for swallowing both Kuangtung and Kuangsi whenever it suits them to start a local rebellion or three.
They receive anyone rowdies for choice, and whole villages join the church and defy their neighbors and their authorities."
25 In his work on the origins of the Boxer movement, Joseph W. Esherick also provides revealing evidence of the frequent contact between instigators of the rebellion and local missionaries in the late nineteenth century.26
Paradoxically, in Gao Shu's 高树 (1848–1931) Trivial Records of a Golden Bell (Jin luan suo ji 金銮琐记), he records that Gang Yi 刚毅 (1837–1900) recommended that President of the Board of Justice Zhao Shuqiao 赵舒翘 (1848– 1901) travel to Zhuozhou to “investigate the Boxers and secretly invite them to enter Beijing."
Soon after, “the Boxers swarmed into the city and busied themselves with burning and killing.
There were close to a hundred good people living outside the city wall who were accused of being members of the White Lotus sect whom the Boxers murdered in the market.
Shuqiao did not save them, but simply said it was their bad luck."
27 Why did the Boxers not describe their victims as believers in a foreign religion? If Gao's record is true, then the ‘Boxer bandits' perceived the White Lotus sectarians as their competitors. If the record is false, it still illustrates that scholars projected onto the Boxers a belief in the equivalency of Christian and White Lotus beliefs.
As early as 1844, Zhang Mu 张穆 (1805–1849) refuted the “equation of Catholicism with White Lotus sectarianism" emphasizing the essential differences between the two religions, which illustrates the early origin of such ideas.28
Based on the above evidence, it seems valid to say that many Chinese regarded Christianity as heterodox along with White Lotus and Eight Trigram sectarianism.
Despite the protection of the Unequal Treaties, contacts between missionaries and Chinese scholars remained limited until the turn of the twentieth century.
Judging from the observations of Li Hongzhang, Song Shu, Xu Kunxi, and Zhang Taiyan, Liang Qichao's statement that “several hundred years after the arrival of Christianity the number of upperclass converts is limited" remained true for some time after 1900.
29 The cultural competition between China and the West unquestionably impacted the number of Chinese converts to Christianity. Most Chinese ‘Christians' who did convert did so because of the special social functions of Christianity in China. As the Taiping Rebellion revealed, when forced to consider the relative importance of the two dichotomies, China/West or civilized/barbarian, Chinese scholars focused on the latter."""
```


## Batch processing & evaluation

The following example shows how to use Bertalign to align the Text+Berg corpus, and evaluate its performance with gold standard alignments. The evaluation script [eval.py](./bertalign/eval.py) is based on [Vecalign](https://github.com/thompsonb/vecalign).

Please see [aligner.py](./bertalign/aligner.py) for more options to configure Bertalign.

```python
import os
from bertalign import Bertalign
from bertalign.eval import * 
```

```python
src_dir = 'text+berg/de'
tgt_dir = 'text+berg/fr'
gold_dir = 'text+berg/gold'
```

```python
test_alignments = []
gold_alignments = []
for file in os.listdir(src_dir):
    src_file = os.path.join(src_dir, file).replace("\\","/")
    tgt_file = os.path.join(tgt_dir, file).replace("\\","/")
    src = open(src_file, 'rt', encoding='utf-8').read()
    tgt = open(tgt_file, 'rt', encoding='utf-8').read()

    print("Start aligning {} to {}".format(src_file, tgt_file))
    aligner = Bertalign(src, tgt, is_split=True)
    aligner.align_sents()
    test_alignments.append(aligner.result)

    gold_file = os.path.join(gold_dir, file)
    gold_alignments.append(read_alignments(gold_file))
```

    Start aligning text+berg/de/001 to text+berg/fr/001
    Source language: German, Number of sentences: 137
    Target language: French, Number of sentences: 155
    Embedding source and target text using LaBSE ...
    Performing first-step alignment ...
    Performing second-step alignment ...
    Finished! Successfuly aligning 137 German sentences to 155 French sentences
    
    Start aligning text+berg/de/002 to text+berg/fr/002
    Source language: German, Number of sentences: 293
    Target language: French, Number of sentences: 274
    Embedding source and target text using LaBSE ...
    Performing first-step alignment ...
    Performing second-step alignment ...
    Finished! Successfuly aligning 293 German sentences to 274 French sentences
    
    Start aligning text+berg/de/003 to text+berg/fr/003
    Source language: German, Number of sentences: 95
    Target language: French, Number of sentences: 100
    Embedding source and target text using LaBSE ...
    Performing first-step alignment ...
    Performing second-step alignment ...
    Finished! Successfuly aligning 95 German sentences to 100 French sentences
    
    Start aligning text+berg/de/004 to text+berg/fr/004
    Source language: German, Number of sentences: 107
    Target language: French, Number of sentences: 112
    Embedding source and target text using LaBSE ...
    Performing first-step alignment ...
    Performing second-step alignment ...
    Finished! Successfuly aligning 107 German sentences to 112 French sentences
    
    Start aligning text+berg/de/005 to text+berg/fr/005
    Source language: German, Number of sentences: 36
    Target language: French, Number of sentences: 40
    Embedding source and target text using LaBSE ...
    Performing first-step alignment ...
    Performing second-step alignment ...
    Finished! Successfuly aligning 36 German sentences to 40 French sentences
    
    Start aligning text+berg/de/006 to text+berg/fr/006
    Source language: German, Number of sentences: 126
    Target language: French, Number of sentences: 131
    Embedding source and target text using LaBSE ...
    Performing first-step alignment ...
    Performing second-step alignment ...
    Finished! Successfuly aligning 126 German sentences to 131 French sentences
    
    Start aligning text+berg/de/007 to text+berg/fr/007
    Source language: German, Number of sentences: 197
    Target language: French, Number of sentences: 199
    Embedding source and target text using LaBSE ...
    Performing first-step alignment ...
    Performing second-step alignment ...
    Finished! Successfuly aligning 197 German sentences to 199 French sentences

```python
scores = score_multiple(gold_list=gold_alignments, test_list=test_alignments)
log_final_scores(scores)
```

     ---------------------------------
    |             |  Strict |    Lax  |
    | Precision   |   0.932 |   0.987 |
    | Recall      |   0.941 |   0.991 |
    | F1          |   0.936 |   0.989 |
     ---------------------------------

## Citation

Lei Liu & Min Zhu. 2022. Bertalign: Improved word embedding-based sentence alignment for Chinese–English parallel corpora of literary texts, *Digital Scholarship in the Humanities*. [https://doi.org/10.1093/llc/fqac089](https://doi.org/10.1093/llc/fqac089).

## Licence

Bertalign is released under the [GNU General Public License v3.0](./LICENCE)

## Credits

##### Main Libraries

* [sentence-transformers](https://github.com/UKPLab/sentence-transformers)

* [faiss](https://github.com/facebookresearch/faiss)

* [sentence-splitter](https://github.com/mediacloud/sentence-splitter)

##### Other Sentence Aligners

* [Hunalign](http://mokk.bme.hu/en/resources/hunalign/)

* [Bleualign](https://github.com/rsennrich/Bleualign)

* [Vecalign](https://github.com/thompsonb/vecalign)

## Todo List

- Try the [CNN model](https://tfhub.dev/google/universal-sentence-encoder-multilingual/3) for sentence embeddings
* Develop a GUI for Windows users
