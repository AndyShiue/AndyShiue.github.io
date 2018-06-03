直構邏輯的崛起
The Rise of Intuitionistic Logic

零、前言
　　Preface

我要最先感謝接受我入學申請的清華大學。我能進入清華大學並非藉由大型考試，而是透過一尋找擁有特殊專長學生的管道。我的專長是程式語言和邏輯，而這也是本報告的主題。

First of all, I want to express my gratitude to National Tsing Hua University (NTHU)  for accepting my application of enrollment without my taking the ability test, but through an independent program to find students who have special skills, and my specialty is about programming languages and logic, which are the topics of this essay.

有趣的是，儘管這是我們大學一年級生在華語課上必備的報告，我在一開始就便用英文撰寫這篇文章，而後才翻譯回華語。或許這是因為以前幾乎沒有這方面的華語資源所以我在某些特定的主題上較習慣使用英文。

Interestingly, although this is the required essay for our freshman Mandarin course, I wrote the whole of it in English first and translated back to Mandarin, perhaps because there was almost no Mandarin resources of this kind so I was used to English in these specific topics.

儘管良好的直覺肯定是有幫助的，整篇報告的目標客群是完全沒有直構邏輯背景的讀者。在閱讀完這篇報告之後，若讀者能瞭解直構邏輯的好處或更進一步深入探討這領域，那將會是我的榮幸。

This whole essay is intended for readers without any background of intuitionistic logic, though some common sense would indeed be useful. After finishing reading this essay, It would be my pleasure that the reader would be able to know the good parts of intuitionistic logic, or even better, to dive into this area.

一、總覽
　　Overview

自古以來，人們一直努力發掘數學的嚴謹根本，其中較進階的概念被建構於較基本的之上，而最終歸於一套獨立的基石，也就是數學邏輯，其下為無法被標準化解釋的哲學，其上則為所有正規數學。

Since antiquity, there has been certain efforts being put on rigorous bases in math, which, eventually led to some standalone foundation, namely mathematical logic, between non-formalizable philosophy and all formal math, whereas more advanced concepts in math are defined within the system from more basic constructs.

系統中除了要有定義新（數學）物件的能力，能觀察物件之間互動的能力或許更像是一般人對「邏輯」一詞的認知。在各式各樣的數學邏輯中，最被廣泛接受的大概是處理因果律的命題邏輯，其中或許能被派生的規則有鏈鎖律或雙重否定律；鏈鎖率聲明若一果即是一因，則那前一個因導致更後面的果，雙重否定律則說，若一件事不為假，則其為真。

In addition to having the ability to define new (mathematical) objects in a system, there also has to be some way to observe their interactions, perhaps closer to the common perception of what ‘logic’ means. From what constitutes varieties of mathematical logic, propositional logic is probably the most widely-accepted framework, reasoning about causes and effects. Some implications of it could be the chain rule, that if p causes q and q causes r, then p causes r, or the double negation rule, which says that something is true if it’s not false.

但邏輯學界在命題邏輯之後產生了分歧；集合論者以無型別的集合作為數學領域的根基，型別論者則預設不同物件屬於某種程度上不相容的不同型別。隨著時間的發展，集合論成為了數學上被使用的標準，即便如此，近代的研究揭露了型別論和集合論相比不可思議的表達能力。

However, after propositional logic, there was a split among schools of logicians. Set theorists build up the domain of math with untyped sets; type theorists, on the other hand, presuppose there are objects of different, somehow incompatible types. As time goes by, set theories have become dominant in math, however, later research has revealed the incredible expressiveness of type theories compared to set theories.

這份報告的目標是對直構型別理論的意義提供一個簡短而不完整的介紹，而後解釋為何它仍不被廣泛使用，儘管在我眼中這是更能被人類直覺理解的邏輯，或許更重要的是，尤其對電腦來說。

This essay aims to provide a brief, incomplete introduction of the meaning of intuitionistic type theory, and why it hasn’t been popular yet despite the logic’s somehow being more “intuitive” for human beings, or perhaps more importantly, especially for computers, in my opinion.

二、公理化數學的濫觴：歐幾里得的幾何
　　The Origin of Axiomatized Math: Euclid’s Geometry

我們先從歷史開始談起並溯及數學的開端。為提供現象的理由，我們進行「演繹」，意即用較簡單的已知事實解釋它。然而，在多次演繹之後，任何被觀測到的現象總要被追溯到某些先驗知識，那些只能被視為理所當然的先驗知識。柏拉圖式的觀點認為數學是現實的理想化，因此在數學中假設某些第一因即「公理」存在似乎再自然不過，公理和演繹規則便構成了基本概念背後的準則。

We start from history and trace back to the inception of math. In order to provide some reason to a phenomenon, we explain it from simpler known facts, the process of which is called “deduction”. However, after rounds of deduction, any observation would ultimately be traced back to some a priori knowledge, that can only be taken for granted. Math, from a platonic view, is the idealization of the reality, and it seems natural enough to assume first causes, called “axioms”, exist in math and serve as the laws of the primitive notions along with the deduction rules.

古希臘的數學家歐幾里德是一位採用公理化方法的先鋒，他以五條公理作為他發展出的幾何學的基礎，儘管後來人們知道他使用了很多未提及的公理，類似的公理化方法之後仍獲得了巨大的成功。

Euclid, the ancient Greek mathematicians, pioneered in using axiomatized method to provide a basis of his geometry and attempted to conclude his discovery with 5 axioms. Although the axioms are later known to be far from complete, this kind of methodology has seen great success.

儘管現在的數學系學生可能會認為自然數的公理較易被理解，對自然數的公理化在相較起來很晚的1889年才被皮亞諾完成。

Even though students in math nowadays would probably think it’s easier, the axiomatization of natural numbers happens much later in the history of math, by Peano in 1889.

三、形式主義：數學僅是符號操作
　　Formalism: Merely Manipulating Symbols

同時間，撰寫數學使用的語法也在不斷地演進，舉例來說，括號在1544年被導入，而等號在1557年被導入。自從19世紀末，數學的核心，也就是數學邏輯，也終於緩緩地被符號化。「數學中的所有概念都能被以符號形式化」，這樣的想法讓人們對數學採取了激進的視角：

> （數學）更像是一場遊戲，和飛行棋還有西洋棋相比，它並不更多地偕同對物件或性質本體的印證。

The syntax to write math was also evolving at the same time. For example, parentheses were introduced in 1544, and the equal sign was introduced in 1557. Since late-19th century, the core of math, namely its logic, was eventually getting symbolized gradually. That everything in math is formalizable as symbols has led to a radical view on math, that

> (math) is much more akin to a game, bringing with it no more commitment to an ontology of objects or properties than ludo or chess.
> (https://plato.stanford.edu/entries/formalism-mathematics/)

諷刺的是，他們似乎否認自古希臘以來的柏拉圖主義，在柏拉圖主義中，數學被認為用來表示物理實體背後完美、理想的物件。也就是說形式主義是......

It sounds like there’s some ironic defiance over the ancient Greek platonism, in which math is thought to represent perfect, ideal objects behind physical ones. Which means formalism is ...

> ......將數學視為在紙上用標記玩著根據規則、無意義的正規遊戲的人。形式主義哲學能被追溯到喬治·貝克萊，但它主要的擁護者為大衛·希爾伯特......

> ... the view that mathematics is a meaningless formal game played with marks on paper, following rules. Traces of a formalist philosophy of mathematics can be found in the writings of Bishop Berkeley, but the major proponents of formalism are David Hilbert (1925) ...
(Philosophy Mathematics, Ernest)

四、希爾伯特之夢
　　David Hilbert’s Dream

將數學視為如棋類遊戲的視角將不可避免地導向一個目標，即尋找這個遊戲最好的規則。1900年左右數學家希爾伯特願發展的綱領有著這樣的宏願。希爾伯特想要找到一組數學規則，滿足這樣的兩個性質：

1. 一致的，且
2. 完備的

一個理論是一致的若任何導出的陳述都不能同時被證明為對的和錯的；完備的若任何陳述都能證明為對的或錯的。前者似乎像是一個比較基本的要求，因說一個陳述既對且錯在直覺上是無理的，但後者從哲學的角度看必定較難：如果你將道德視為一場遊戲，那麼你必須確保你能從基本推論中鑒別出正義與否。人們曾認為在數學上鑒別事物的對錯可能較簡單，天真的想法是，在找到一條無法被鑒別的陳述後，把它加入規則中，就像在找到道德上的灰色地帶時將其劃分到其中一邊。這是希爾伯特的夢，他想為數學提供堅若磐石的完美基礎，遺憾的是，這後來被證明是不可能被實現的。

The perspective of math as a game would inevitably lead to a goal: to find the best rules of the game. The program led by mathematician David Hilbert around 1900 had such grand goal. Hilbert wanted to find some rules of math that is both

1. consistent, and
2. complete

A theory is consistent if any derived statement cannot be proved as both right and wrong; a theory is complete if every statement can be proved as either right or wrong. The former seems like a more basic requirement because saying something is both right and wrong is always utter nonsense at first sight. The latter would definitely be harder from the point of view of philosophy: if you view morality as a game, then you have to make sure you can identify anything as either justice or not from some basic arguments. It was thought that maybe it was easier to do something similar to math to make everything either true or false. The naïve plan is to add the newly-discovered undecidable statements as new rules. It’s like adding some act as a rule of morality if it was previously in the gray area. This is Hilbert’s dream, to provide a solid foundation that is guaranteed to be perfect for math. It was a pity that it was later proved to be impossible.

哥德爾在1931年發表了這樣的成果。他的第一定理告訴我們一個有用的系統（「遊戲規則」）是不可能既一致又完備的。更糟的是，他的第二定理告訴我們，就連想在那樣的系統裡證明自身的一致性都不可行。

Kurt Gödel published such result in 1931. His first theorem stated it’s impossible for a useful system (“rules of game”) to be able to be both consistent and complete. What’s worse is that, his second theorem states it’s not even possible to prove the consistency of the rules inside the same system.

我們只能相信系統的一致性，但第一定理告訴我們不應該尋求一個完備的理論，而該尋求一合情合理的。一派數學哲學家對挑選這樣的規則有著某些準繩，也就是，不追求真實性，而追求可建構性。

We can only believe in the consistency, but the first theorem suggests we shall not find a complete theory, but a reasonable one, and members in one school of mathematical philosophy has some criteria for choosing such rules, that is, not to be true, but to be constructive.

這是我的觀點，也是我要進行的論述。這是直構主義。

This is my opinion, and also the topic I want to discuss about. This is intuitionism.

五、追求真實的古典邏輯和追求正確的直構邏輯
　　Classical Logic for the Truth, Intuitionistic Logic for the Right

最初，直構主義就是指基於直覺的數學。直構主義的先鋒，魯伊茲·布勞威爾把直構主義描述為：

> 完全把數學和數學的語言亦即邏輯描述語言的現象分離開來，了解到直構數學根本而言是一個心靈上而無語言的行為，那樣的行為基於對時間流逝的感知。這樣對時間流逝的感知或許能被描述為人生中的一瞬被撕裂成兩個不同的物件，其一被另一所取代，但仍殘餘在記憶中。若取走這初生兩者的質地，它便進入了這所有二元性的，空理型的共同基質；這是共同的基質，是空理型，是對數學的根本直觀。

At the beginning, intuitionism is literally, based on intuition. The pioneer of intuitionism, L. E. J. Brouwer, described intuitionism as:

> Completely separating mathematics from mathematical language and hence from the phenomena of language described by theoretical logic, recognizing that intuitionistic mathematics is an essentially languageless activity of the mind having its origin in the perception of a move of time. This perception of a move of time may be described as the falling apart of a life moment into two distinct things, one of which gives way to the other, but is retained by memory. If the twoity thus born is divested of all quality, it passes into the empty form of the common substratum of all twoities. And it is this common substratum, this empty form, which is the basic intuition of mathematics.
> (Brouwer's Cambridge lectures on intuitionism)

在當時，直構主義並非形式主義也非柏拉圖主義，但隨著時間過去，它們開始融合而直構主義慢慢變成了構造主義的同義詞。近代，直構主義者也接受了形式主義的處理方式：把規則編碼成一串符號並操作那些組合成的公式。即便如此，可構造性還是，也一直都會是讓直構數學與傳統數學不同的精華之處。

At that time, intuitionism is the same as neither formalism nor platonism, but as time goes by, they started to converge as a whole and intuitionism has gradually become synonymous with constructivism. Nowadays, intuitionists are also fine with the formalistic approach: to encode rules as sequences of symbols and manipulate those formulas. However, constructivity still and will still stand as an essential feature that makes it different to traditional math.

以下，我將要介紹一個何謂構造性，或者應該說，何謂非構造性的例子。小安是一個暴力又愛說謊的小孩子，所以她的父母為了教育她設立了兩條規則。

1. 和其他人打架要被懲罰
2. 說謊要被懲罰

現在給讀者的問題來了，如果小安對她的父母說，「我揍了小勝一拳。」請問小安要被懲罰嗎？

Below, I’m going to introduce an example to describe what constructivity, or rather, what non-constructivity is. Let’s say Anne is a violent little kid who is used to lying. Anne’s parents set out two rules for her to teach her the polite behavior.

1. Fighting with the others makes Anne get punished.
2. Lying makes Anne get punished.

Now, if Anne said to one of her parents, “I punched Shen.” The reader should think for a while now, that should Anne be punished?

根據古典邏輯，小安必定要被懲罰。我們知道小安要不是在說謊話就是說實話，如果小安在說謊，那麼她要因說謊被處罰，他如果他說的是實話，她則要因打人被處罰。

According to classical logic, Anne must be punished. We know Anne is either lying or not. If she is lying, then she must be punished due to it, but if not, she must be punished for fighting.

可是如果你是小安的父親而這兩種行為應要受到不同的懲罰，你要怎麼懲罰小安？上述的演繹中只提到她會被懲罰，卻並未提供任何懲罰的具體方法。這麼一來，在要求構造性且沒有更進一步證據的前提下，小安該被懲罰的事不應該是能被證明的，因我們無法構造這般懲罰。或許小安要被懲罰是事實，但我們還不知道正確的方式，而這是構造式數學的精髓。

However, assuming the two bad acts ought to receive different sorts of punishment, how should you punish Anne if you were her father? In the above deduction, it merely says she will be punished without providing any concrete method to do it. Therefore, in the constructive outset, it should not be provable that Anne will be punished without any further evidence given that we cannot construct such punishment. It might be true that Anne will be punished, but there hasn’t been a correct way to do it, and this is the gist of constructive math.

我們能說在構造式數學裡，

* 如果你想證明一個因果關係，你必須要有一個過程，一個將因變為果的轉換方式。
* 如果你想證明某個存在，你必須要有一個特定的實例。
* 如果你想證明一個或另一個陳述是真的，那你必須闡明究竟何者為真

We can say that in constructive math,

* If you want to prove an implication, there must be some procedure, namely how the cause is transformed to the outcome.
* If you want to prove an existence, there must be a specific instance.
* If some statement or another is true, then the one that is really true must be specified.

在上面小安的例子中，哪一個選項為真是未被闡明的，這麼一來，構造性就被破壞了。問題在於，我們天真地假設任何陳述若非真的，就是假的，這和先前我提到的雙重否定律有異曲同工之妙，雙重否定律說，如果一件事的反面是錯的，則它是對的，但沒有任何佐證被提出。這些是非常合理的揣測，但同時也一點都不具構造性：我們就是無法解釋為什麼如此這般，要怎麼解釋反之的結果是正確的？而可解釋性就是可構造性。順帶一提，我前幾次提到「真實」時用的也非古典意義上的意思，而是指「能被構造的」。

In the above example about Anne, the option about the truth not being specified breaks constructivity. The core issue is that, we naïvely assume any statement must be false if it isn’t true; this shares the similarity to the aforementioned double negation rule, which says if the opposite of something is wrong, then it’s right, without giving an evidence. These are very reasonable speculations, but at the same time aren’t constructive at all: we simply can’t explain why it is so and how the opposite can be explained, and explainability is constructability. By the way, the last several usage of the word “truth” above is not in a classical sense, but has the meaning of “being constructable”.

六、柯里—霍華德同構
　　Curry-Howard Isomorphism

從上面對構造性意義的解釋中，你可能會注意到因果關係在根本上就只是函數，或轉換，如果你傾向使用這個詞。在這樣的詮釋中，陳述的可證明性被視為和數字或向量並無二致的數學物件，而因果關係就只是函數的特例：它是一將陳述轉換成另一陳述的函數。這是證明的世界與程式的世界最顯而易見的一個連結，而這道完整的橋被稱為「柯里—霍華德同構」

From the above introduction of constructivistic meaning, you may notice that implication, by its nature, is just a function, or transformation, if you prefer this terminology. In this kind of interpretation, provability of statements are viewed as mathematical objects indifferent from numbers of vectors, and implication is just a special case of a function from a statement to another. This is the most obvious link between two fields, proofs and programs, connected with the bridge “Curry-Howard isomorphism”.

首先，我要說很多定理都分別有很多種不同的定義方式；我們可以把一個有證明的定理視為一有元素的型別。證明和元素都是其擁有者的性質，而或許我們能更激進，說元素就是證明，或如果你偏愛更好的詞彙的話，元素是對型別的一「見證」。這樣，型別就會是陳述，因型別有元素而陳述有證明。「柯里—霍華德同構」這個可怕的名稱只不過是這樣概念的術語罷了。

First I want to say, lots of theorems have very different proofs for each of them. It would be possible to view a theorem having proofs as a type having elements. Proofs and elements are properties of its owner, and maybe we can be more aggressive, to say that elements are exactly proofs, or an “evidence” of such type, if you prefer this better word. Hence, types are statements in the sense that types have elements and statements have proofs. The scary name “Curry-Howard isomorphism” is just a jargon for such concept.

回到比較理論的部分，我們說真實是任何「有居民」的型別，而虛假則是空型別，因其缺少「證人」。一個陳述的相反被合理地定義成從論述轉換到虛假的函數。虛假就是荒謬的、矛盾的，因為它是我們最不想證明的。我們說一陳述是錯的若它能導致矛盾，而這也被寫作它的相反為正確的。

Back to some theoretical part, we say truth is any inhabited type, and falsity is the empty type due to its lack of evidence. The negation of a statement is defined reasonably to be a function from the statement to the falsity. The falsity is the same as absurdity, or a contradiction, and it is the thing we want most not to be able to prove. We say some statement is wrong if it can deduce a contradiction, and this is also written as its opposite being right.

如果事情非對即錯，這代表如果我不能證明一陳述正確，則它一定要是空無（沒有證據）的，因為它能被轉換成空無。可惜，在這樣的情境下「它必定是空無的」是非建構式的說法。

If things are either right or wrong, this would mean for a statement we can’t prove to be right, it must be empty (having no evidence) because it has a function into emptiness. However, in this situation the “it must be empty” part isn’t constructive.

函數，或者說是轉換，正是程式編寫中的核心。數年前，我驚嘆於數學和程式之間的關係能融合得那麼好；在這樣直構邏輯的一體中，程式與證明的搭配簡直天衣無縫。我們能在統一的語言裡撰寫程式，稍後再補上對它們某些性質的證明，或者我們能在函數於電腦上運行前要求提供一個證明。所有的這些，對大學生來說已經是個夢了，在傳統邏輯中，我們完全沒有這種好處。可惜，全世界的學生還是被教授著古典邏輯。以我的觀點來看，不教學直構邏輯遲滯了清華大學正極力推廣的跨領域教育，至少在某些部分上。

Functions, or to say transformations, is exactly the core of programming. I was amazed at how math and programming fit together so well several years ago. In this unified world of intuitionistic logic, programs and proofs work seamlessly. We can write programs in the unified language and later prove some of their properties, or we can require some proof for some function to be run on the computer. All of these, is already a dream for the undergraduates nowadays. In the traditional setting, we have nothing like this. However, classical logic is still what students are being taught in the world. In my opinion, not teaching intuitionistic logic stagnates the interdisciplinary education that’s been on hype in NTHU, at least in some parts.

七、為何直構邏輯並不成功？
　　Why isn’t intuitionistic logic a success?

根據我的經驗，直構邏輯並不真正成功應要從兩個面向被解釋。一是從程式員的觀點，二則是從數學家的觀點。

From what I see, the reason why intuitionistic logic isn’t really successful can be split into two parts: from the point of view of programmers, and from that of mathematicians.

以程式員那一方來說，真正使用到直構邏輯的程式語言一般被認為太難。第一是因為目前程式編寫的主流典範是物件導向式的，而非偏向直構邏輯的函數式程式；第二，設計程式語言的大公司可能會為了試圖讓不真正專業的程式員，或者說是讓每個人都能寫程式，而在語言設計上顯得保守，Google的Go程式語言便是一例。

On the side of programmers, programming languages that make extensive use of intuitionistic logic is often perceived as being too hard. Firstly because the current dominant paradigm of programming is still Object-Oriented Programming (OOP), not the functional programming that leans toward intuitionistic logic more. Second, there’s a tendency to make everyone able to write the code, without the need to be really professional. This could make big companies be conservative about their designing programming language, such as the Go programming language designed by Google.

然而，現在的趨勢已經在往被認為有較堅實理論基礎的函數式編程方法走。若論及對新手的友善程度，我們則能反觀某些在業界受到廣泛使用卻非常困難的程式語言，例如C++；更進一步來說，如果你不想在程式中進行證明，你有不這麼做的權力，而在C++中某些陷阱卻是不可避免的。因此，我認為那樣複雜的邏輯系統並非真正是其產業化的阻礙。

However, the current trend is already going towards functional programming, that is considered to have a more solid theoretical foundation. When it comes to beginner-friendliness, there are already very difficult programming languages widely adopted in the industry such as C++. Moreover, if you don’t like to prove stuff in programming, you have the right not to do it, and in the case of C++ there are in contrast footguns that are unavoidable. Thus, I think such complex logic system isn’t much of an obstacle for its industrialization here.

我想在數學上它未被廣泛採用真正最重要的原因是是它在歷史上較緩慢的發展。二十世紀初的人們似乎沒有意識到直構邏輯的重要性；或許主要的原因是那時電腦甚至還未被發明，而且那樣的邏輯系統需要更精緻的處置方法。在集合論成為數學的基礎之後，社會就被固化了。這和物件導向在程式設計中的狀況一樣，它們就只是先壟斷了市場。

I think the actual major reason that intuitionistic logic isn’t widely adopted in math is its slower development in history. People in the early-20th century seemed not to realize the importance of intuitionistic logic. Maybe the main reason is that computers weren’t even invented yet at that time and such logic system needs more sophistication. After set theory came out as the foundation of math, the society simply got stuck, which is similar to the situation in programming with OOP. They are just monopolizing the market first.

不過程式設計的風向已經正在變化；湯瑪斯·孔恩曾提出所謂「典範轉移」的概念，隨著時間過去，科學（在此，數學）社群可能會突然轉變，轉變成以非常不同的方式看待事物，而我相信因電腦的重要性正日益提升，那一天終將來臨。

However, the situation in programming is changing. Thomas Samuel Kuhn introduced the concept of paradigm shift, that over time the scientific (here, mathematical) community could be abruptly transformed to perceive things in a very different way, and I believe given the increasing importance of computers, that day will finally come.

附錄一、直構邏輯可能的應用
　　　　Possible applications of intuitionistic logic

以傳統的做法來說，通過所有測試案例是對是驗證程式正確性的方式。然而，這只能找到程式錯誤的部分，卻無法確定它是絕對正確的。若運用了某些直構邏輯，我們能知道它不可能出錯。

In the traditional approach, verification of a program is done by passing all the test cases. However, this can only spot the incorrectness of the program, but not guaranteeing it’s really done right. By utilizing some intuitionistic logic, we can know it doesn’t go wrong for sure.

在我看來，直構邏輯或能在幾種不能出錯的產業中得到應用。舉例來說，像是航太工業，銀行系統，或者目前程式界最夯的話題：區塊鏈。區塊鏈是沒有中央機構的虛擬貨幣。儘管要證明程式符合所有規格的成本可能非常高，我還是希望關於證明的技術能被廣泛採用，因為某些自私的原因：我對這部分有興趣也擅長於此。

In my opinion, intuitionistic logic could be used in several sectors that are not allowed to go wrong, such as the aerospace industry, banking systems, and one of the hottest topic in the field of programming currently – blockchains, witch are virtual currencies without a controlling authority. Although the cost of proving all the specifications could be very high, I still hope proving techniques will be adopted widely, due to the selfish reason that I’m interested in it and good at it.

附錄二、不同的同一性——對未來的展望
　　　　Multiple Identities – The Prospect

在這個小節，我想稍稍一探目前的尖端研究領域。在現代直構邏輯中很重要的一個分支是「高維型別理論」。高維型別理論圍繞著相等性的概念進行。以下，我將要述說一個古老的哲學問題；我並不想給出這個問題的正解，只想提供一個定義相等性是什麼究竟有多困難的佐證。

In this section, I want to provide a glimpse of the cutting-edge research area. A quite important branch in modern intuitionistic logic is the so called “higher-dimensional type theory”, which is centered on the concept of equality. Below, I’m going to tell an old philosophical problem, not to argue about the correct solution to it, but to demonstrate the actual difficulty of defining what equality is.

有一艘用木頭做的船。隨著時間過去那艘船慢慢腐爛掉了，而腐爛的部分會被新的材料所取代。在所有舊木材都被新的部分取代之後，新的船還是那艘舊的船嗎？

Let’s say there’s a ship made of wood. As time goes by, the ship slowly got rotten, and those rotten parts would be replaced by the new materials. After all old woods of the ship have been replaced by new pieces, is the new ship still the the original one?

不同的哲學家有不同的意見，而我不會談論它們之中的任何一種。但因為可能有對相等性一概念的不同詮釋，為何不讓任何人有定義他們所謂相等性的能力？同樣地，一個相等性或許也能被視為某個數學上的物件，而如果有人說兩物是相等的，他們能選取他們偏好的概念而指明它們以什麼角度觀看這個世界。基本上，這是把決定的權利交給人民。或許這是對高維型別理論最重要的直觀解釋

Different philosophers’ opinion diverge, and I won’t discuss about any of them. But since there could be different interpretation of what equality is, why not make it possible for anyone to define their equalities? Again, an equality could also be seen as some mathematical object and when someone says two things are equal, they can specify in what sense they are by picking the notion they prefer, and it basically defers the right to decide to the people. Perhaps this is the most important intuition for higher-dimensional type theory.

然而，這些不同人定義出的相等性不一定是相等的，這暗示了我們可能有兩個相等的相等性，也就是說能有相等性的相等性。我們可以繼續下去並構造更高的相等性。

However, those sorts of equalities defined by different people are possibly not equal; this suggests there could be two equal equalities, or equalities of equalities. We can even go on and on and construct higher equalities.

就像我們之前把證明和元素視為一體兩面，在高維型別理論中有著所謂三位一體，元素或證明再度被視為空間中的一點，而一個簡單的相等性能被視為兩點之間的一線。那些更高的相等性則可以是二維或更高維的面，而這所有概念能被用來建造空間的全域形狀，這是為什麼它被稱為高維型別理論的原因。

Much like our viewing proofs and elements as two ways of describing the same thing, in higher dimensional type theory, elements or proofs are again viewed as points in a space as a trinity, and a simple equality could be viewed as a line between two points. Those higher equalities can be two-or-more-dimensional faces and can be used to build the globular shape of a space, hence the name higher-dimensional type theory.

對非本領域的讀者來說，這一節可能太難。不過，我仍在此報告中提及了它，希望有人能被吸引而進入這初生的領域。

This section might be too hard for a reader who isn’t in this field, however, I included it in this essay, hoping to attract someone to go into this fledgling field.
