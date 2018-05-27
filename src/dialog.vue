<template>
    <div v-if="showModal">
        <transition name="fade">
            <div class="modal-mask">
                <div class="modal-wrapper">
                    <div class="modal-container">
                        <div class="modal-header">
                            <h3 class="title">{{ displayTitle }}</h3>
                            <button class="closeBtn" @click="closedialog">
                                <i class="fa fa-times" aria-hidden="true"></i>
                            </button>
                        </div>

                        <div class="modal-body">
                            <iframe width="100%" frameborder="0" scrolling="no" marginheight="0" marginwidth="0" src="https://www.openstreetmap.org/export/embed.html?bbox=121.83258357588785%2C25.079819843048295%2C121.84644523207682%2C25.091888136619303&amp;layer=cyclemap"></iframe>
                            <div class="imgGroup" v-for="(pic, index) in displayImg" :class="'direction' + imgdirection[index]">
                                <transition name="fade">
                                    <img :src="pic" v-on:load="imgOnLoaded" v-show="imgLoaded"/>
                                </transition>
                                <p>
                                    {{picText[index]}}
                                    <span v-if="imgResouce !== ''">{{ imgResouce }}</span>
                                </p>
                            </div>
                            <div class="textGroup" v-html="displayText"></div>
                            <div class="subTextGroup" v-html="displaySubText"></div>

                        </div>
                    </div>
                </div>
            </div>
        </transition>
    </div>
</template>
<script>
export default {
    props: ["show", "type"],
    data() {
        return {
            showModal: this.show,
            displayTitle:'',
            displayImg:[],
            imgdirection:[],
            imgResouce:'',
            imgLoaded: false,
            picText:[],
            displayText:'',
            displaySubText:''
        };
    },
    watch: {
        show: function () {
            this.showModal = this.show;
            this.updatedialog();
        }
    },
    methods: {
        closedialog() {
            this.showModal = false;
            this.$emit("close");
        },
        imgOnLoaded() {
            this.imgLoaded = true;
        },
        updatedialog() {
            var vm = this;
            switch(this.type) {
                case 1:
                    vm.displayTitle = '瑞芳｜金字碑古道';
                    vm.displayImg = [require('./assets/1-1.jpg'), require('./assets/1-2.jpg'), require('./assets/1-4.jpg'), require('./assets/1-3.jpg')];
                    vm.imgdirection = [1,1,0,0];
                    vm.imgResouce = '照片來源：新北市觀光旅遊局《新北登山小旅行》';
                    vm.picText = ['金字碑', '金字碑古道入口處', '探幽亭及奉憲示禁碑', '金字碑古道出口'];
                    vm.displayText = '<p>昔日淡蘭古道(官道)的路線之一，海拔標高約550公尺，全長約2公里，為從前古人往來瑞芳與宜蘭之間的山徑，在淡蘭古道開通之初，當時的鎮臺總兵劉明燈率兵北巡，於陡峭山壁題詩，用以鎮守壓嚴峻的氣候，後人將金箔塗於石壁銘文上，因而流傳「金字碑」的美名至今。</p><p>自淡蘭橋與天煌亭進入古風之旅，一步步踩踏著石階，耳畔旁傳來陣陣平溪線火車低鳴的汽笛聲，在林木濃蔭中穿梭，感受多元生態的豐富樣貌，途經金字碑探幽亭與奉憲示禁碑，隨即迎接地是基隆嶼與瑞濱一帶的壯闊視野，置身其中的清幽寂靜，讓時光仿若凍結。</p>';
                    vm.displaySubText = '<h6>周邊景點：</h6><p><a href="https://tour.ntpc.gov.tw/zh-tw/Attraction/Detail?wnd_id=60&id=110748">猴硐煤礦博物園區</a>、<a href="https://tour.ntpc.gov.tw/zh-tw/Attraction/Detail?wnd_id=60&id=110802">猴硐貓村</a>、猴硐生態教育園區</p><h6>延伸閱讀：</h6><p><a href="https://theinitium.com/article/20171122_pickup_Jiufen/">黃金山城裡的歲月風華</a></p>';
                    break;
                case 2:
                    vm.displayTitle = '貢寮｜草嶺古道';
                    vm.displayImg = [require('./assets/2-1.jpg'), require('./assets/2-2.jpg'), require('./assets/2-3.jpg'), require('./assets/2-4.jpg')];
                    vm.imgdirection = [0,0,0,0];
                    vm.imgResouce = '照片來源：新北市觀光旅遊局《新北登山小旅行》';
                    vm.picText = ['每年11月過後莫嶺古道的芒草奇景', '虎字碑', '啞口觀景亭', '雄鎮蠻煙碑'];
                    vm.displayText = '<p>昔日淡蘭古道(官道)的路線之一，海拔標高約342公尺，全長約8.5公里，橫跨新北市貢寮與宜蘭縣頭城的交界，以南方築路技術為底的青石鋪設而成，經過日據時代的拓展與光復時期的維護，在歷史的洗禮中，造就一座座遺跡的林立。</p><p>沿途景緻別具一番風味，駐足一覽鎮臺總兵劉明燈親筆題字的雄鎮蠻煙碑與虎字碑，身後的喬木漸轉為灌木，夏日的野薑花香漫滿山、秋日的芒花搖曳風中，再邁開步伐至埡口觀景亭登高一望，撥去飄渺的雲霧，將貢寮卯澳與龜山島的沿岸風光盡收眼底。</p>';
                    vm.displaySubText = '<h6>周邊景點：</h6><p>貢寮老街、<a href="https://tour.ntpc.gov.tw/zh-tw/Attraction/Detail?wnd_id=60&id=112781">狸和禾小穀倉</a></p>';
                    break;
                case 3:
                    vm.displayTitle = '石碇｜外按古道(淡蘭古道石碇段)';
                    vm.displayImg = [require('./assets/3-1.jpg'), require('./assets/3-2.jpg'), require('./assets/3-3.jpg'), require('./assets/3-4.jpg')];
                    vm.imgResouce = '照片來源：新北市觀光旅遊局《新北登山小旅行》';
                    vm.imgdirection = [0,0,0,0];
                    vm.picText = ['外按古道石子路', '在溪流中，有一塊巨石，或稱青蛙石、蟾蜍石', '從觀景平台上眺望淡蘭吊橋及雙溪口', '淡蘭吊橋'];
                    vm.displayText = '<p>昔日淡蘭古道(茶道)的路線之一，海拔標高約66公尺，全長約2.4公里，又稱淡蘭古道石碇段，位於新北市石碇雙溪口與石碇老街之間，嘉慶年間知府楊延理領軍開闢廣闊的山區，帶動大大小小聚落發展，為大菁與文山包種茶踏出一條經濟命脈。</p><p>漫步在木棧道上，置身於溪谷之中，魚兒在清澈地古水圳中悠遊，蜻蜓與蝴蝶在綠蔭中的翩然自得，再向前走入，碎石堆砌而成的石板路迎面而來，忽地回到懷古的時光，仿佛遇見熱烈交談的茶農與商人，再現過去北台灣對外貿易的繁榮，當再踏上淡蘭吊橋，仍在舊日與現代之間留戀忘返。</p>';
                    vm.displaySubText = '<h6>周邊景點：</h6><p><a href="https://tour.ntpc.gov.tw/zh-tw/Attraction/Detail?wnd_id=60&id=109630">石碇老街</a></p><h6>延伸閱讀：</h6><p><a href="https://theinitium.com/article/20171211_pickup_Da-nan/">淡蘭古道石碇段：一條收納時空的步道</a></p>';       
                    break;
                case 4:
                    vm.displayTitle = '深坑｜炮子崙登山步道';
                    vm.displayImg = [require('./assets/4-1.jpg'), require('./assets/4-2.jpg'), require('./assets/4-3.jpg'), require('./assets/4-4.jpg')];
                    vm.imgResouce = '照片來源：新北市觀光旅遊局《新北登山小旅行》';
                    vm.imgdirection = [0,0,0,0];
                    vm.picText = ['土角厝', '步道終點位於茶山古道登山口', '炮子崙登山步道口', '涼亭'];
                    vm.displayText = '<p>海拔標高約553公尺，全長約2.5公里，座落於木柵與深坑的交界，先是一片青綠的梯田與茶園映入眼簾，隨即而來的便是古樸的土角厝與石屋，遠眺七星山、大屯山與觀音山，與群山一同環抱大台北都會區，讓人不自覺忘卻塵囂的紛擾。</p><p>方才結束一趟洗滌身心的旅程，前方的茶山古道隨即又開啟一探秘境的冒險，山徑小路裡卻是別有洞天的景緻，一座百年歷史的草厝，裝載著林家的回憶，至今年過八十的林家兄弟仍然隨著大自然的時序種稻製茶，悠然地品味生活。</p>';
                    vm.displaySubText = '<h6>周邊景點：</h6><p><a href="https://tour.ntpc.gov.tw/zh-tw/Food/Detail?wnd_id=59&id=209063">伴山農莊</a></p><h6>延伸閱讀：</h6><p><a href="https://theinitium.com/article/20180501-chashan/">茶山古道：一條與農家共生的步道</a></p>';
                    break;
                case 5:
                    vm.displayTitle = '平溪｜五分山登山步道';
                    vm.displayImg = [require('./assets/5-1.jpg'), require('./assets/5-2.jpg'), require('./assets/5-3.jpg'), require('./assets/5-4.jpg')];
                    vm.imgResouce = '照片來源：新北市觀光旅遊局《新北登山小旅行》';
                    vm.imgdirection = [0,2,2,0];
                    vm.picText = ['從五分山遠眺暖暖等景色', '從高點瞭望台的步道', '從高點瞭望台的步道', '瞭望亭'];
                    vm.displayText = '<p>昔日淡蘭古道(民道)的路線之一，海拔標高約737公尺，全長約3.4公里，沿著平溪、瑞芳和基隆暖暖的交會稜線延伸，以中央氣象局氣象雷達站為指標，走過平坦的木棧道，邁向階梯步道，征服百岳的氣魄油然而生，一望無際的藍天，伴隨基隆嶼與九份金瓜石的點綴。</p><p>春曉的生意盎然、夏夜的星空閃耀、秋色的詩意撩人、冬日的雲霧飄緲，四季的交替為壯麗的景色增添不同的風貌，單車迷乘風追逐挑戰、攝影師沈醉捕捉晨昏，一樣的山巒，望出不一樣的視野。</p>';
                    vm.displaySubText = '<h6>周邊景點：</h6><p><a href="https://tour.ntpc.gov.tw/zh-tw/Attraction/Detail?wnd_id=60&id=110037">十分老街</a>、<a href="https://tour.ntpc.gov.tw/zh-tw/Attraction/Detail?wnd_id=60&id=109612">十分瀑布</a></p>';
                    break;
                case 6:
                    vm.displayTitle = '雙溪｜虎豹潭步道';
                    vm.displayImg = [require('./assets/6-1.jpg'), require('./assets/6-2.jpg'), require('./assets/6-3.jpg')];
                    vm.imgResouce = '';
                    vm.imgdirection = [0,0,0];
                    vm.picText = ['虎豹潭', '虎豹潭2', '虎豹潭步道'];
                    vm.displayText = '<p>海拔標高約450公尺，全長約4.3公里，因被二座山形酷似猛虎和雲豹的山岳環抱而得名虎豹潭，至今已有百年歷史，在翠綠密林之中，沿著北勢溪蜿蜒，閱覽著明治甲辰年間建成的土地公廟，細細品味廟聯的字句：「福為仁者壽，德正境皆美。」。</p><p>古道林蔭怡然，竹林驚鴻點綴，茶園探出淡雅清香，流傳的舊階引著前方景致，又望見溪谷中溪哥、苦花、馬口、石斑等魚兒戲游水裡，夏日暢快、秋日颯爽，如春茶香，讓一年四季皆感雅緻迷人。</p>';
                    vm.displaySubText = '<h6>周邊景點：</h6><p>泰平假日農夫市集、<a href="https://tour.ntpc.gov.tw/zh-tw/Attraction/Detail?wnd_id=60&id=402318">良心菜攤</a></p><h6>延伸閱讀：</h6><p><a href="https://theinitium.com/article/20171122_pickup_Shuangxi/">雙溪：向大地取經，順應自然的生活慢釀</a></p>';
                    break;
                case 7:
                    vm.displayTitle = '樹林｜大棟山、青龍嶺、大同山登山步道';
                    vm.displayImg = [require('./assets/7-1.jpg'), require('./assets/7-2.jpg'), require('./assets/7-3.jpg'), require('./assets/7-4.jpg'), require('./assets/7-5.jpg')];
                    vm.imgResouce = '照片來源：新北市觀光旅遊局《新北登山小旅行》';
                    vm.imgdirection = [0,0,0,0,0];
                    vm.picText = ['大棟山', '青龍嶺', '青龍嶺眺望臺北盆地景觀非常精采，也是著名的夜景勝地', '南寮福德宮', '從南寮福德宮至大同山的登山步道'];
                    vm.displayText = '<p>海拔標高自237公尺、256公尺一路至405公尺，全長約9.5公里，交界於樹林與龜山鄉之間，大棟山綿延絕佳景望，青龍嶺視野遼闊，如一條青龍盤延，而大同山欣賞境內山峰的角度尤其合適。和樹林、山佳、鶯歌火車站皆相距不遠，尤其山佳車站別具一番風味，建於1903年的百年歷史老車站，最初為簡易的木造站房，作為日本人在鶯歌庄山仔腳開採煤礦運輸之用。</p><p>樹林、三峽、鶯歌、土城、林口與龜山沿處風光，登道後一一盡收眼下，步伐中眺景以外、飛舞彩蝶流轉其中，春夏之際，可見許多雌紅紫蛺蝶、紫一文字蝶、紅星斑蛺蝶、大琉璃鳳蝶、黃裳鳳蝶、台灣麝馨鳳蝶等在林中翩翩悠然。除賞蝶雅趣，大棟山擁有絕佳的三角點及一圖根點，日有翠綠、夜有繁光，豐富角度顯現風華，值得一探。</p>';
                    vm.displaySubText = '<h6>周邊景點：</h6><p><a href="https://tour.ntpc.gov.tw/zh-tw/Attraction/Detail?wnd_id=60&id=110301">山佳車站</a>、<a href="https://tour.ntpc.gov.tw/zh-tw/Attraction/Detail?wnd_id=60&id=402118">鐵道地景公園</a></p>';
                    break;
                case 8:
                    vm.displayTitle = '坪林｜金瓜寮魚蕨步道';
                    vm.displayImg = [require('./assets/8-2.jpg'), require('./assets/8-3.jpg'), require('./assets/8-1.jpg')];
                    vm.imgResouce = '照片來源：新北市觀光旅遊局《新北登山小旅行》';
                    vm.imgdirection = [1,1,0];
                    vm.picText = ['金瓜寮魚蕨步道', '保仁宮牌樓', '金瓜寮自行車道'];
                    vm.displayText = '<p>海拔標高約330公尺，全長約2.2公里，穿過蜿蜒道路、途經盎然茶園、嗅聞山谷芬香，邁入夏季避暑勝地金瓜寮溪。金瓜寮魚蕨步道為途經悠然雅境。金瓜是南瓜的閩南語發音，早年先民來此開墾時，在草寮外種植許多南瓜，此處被稱為金瓜寮，而蜿蜒古道也因此得名。</p><p>步道沿著溪畔修築，淙淙溪水親人，伸手一撩起水花、沁涼感染指尖，伴隨陽光閃耀水面，自在欣賞身旁萬物，有鴨、有螃蟹、有昆蟲，盡顯台灣生態豐富盎然之美，怡人古道兩旁有竹林、有杉林、有蕨類，交織成一幅美麗的圖畫。漫步其中，陣陣蟬鳴、蝴蝶集蜜、花香瀰漫，四季如春，讓人不捨離開此般仙境。</p>';
                    vm.displaySubText = '<h6>周邊景點：</h6><p><a href="https://tour.ntpc.gov.tw/zh-tw/Attraction/Detail?wnd_id=60&id=110177">坪林生態園區<a>、<a href="https://tour.ntpc.gov.tw/zh-tw/Attraction/Detail?wnd_id=60&id=402519">金瓜三號</a></p>\
                                        <h6>延伸閱讀：</h6><p><a href="https://theinitium.com/article/20180301_pickup_pinglin/">進擊的坪林：傳統茶鄉的華麗轉身<a></p>';
                    break;
                case 9:
                    vm.displayTitle = '新店｜獅仔頭山登山步道';
                    vm.displayImg = [require('./assets/9-1.jpg'), require('./assets/9-2.jpg'), require('./assets/9-3.jpg')];
                    vm.imgResouce = '照片來源：新北市觀光旅遊局《新北登山小旅行》';
                    vm.imgdirection = [0,0,0];
                    vm.picText = ['以枕木鋪設的步道', '步道出入口', '從觀音洞遠眺鶯歌及三峽地區'];
                    vm.displayText = '<p>海拔標高約858公尺，全長約5.5公里，位於新店區山區的礦窟溪源頭，是新店的最高峰，名列台灣小百岳，其北側峰頂有一等三角點，因山形狀似蹲伏的獅子而得名。古道戰爭歷史豐富，過去是日軍日本發動太平洋戰爭後，囚禁英、美等盟軍戰俘的收容營，於此遺址，如今立有磺窟戰俘營記念碑。</p><p>除此人文意義，獅頭山步道地形與景色更為一絕，起登的獅仔頭山登山口，即可以觀看101大樓及遠方的大屯山，將台北都會區及遠處山峰盡收眼底。自然風貌更是不可忽略，獅仔頭山步道植物種類繁多，四季斑斕綻放。每年三、四月間可賞金毛杜鵑，其盛名程度，享受愜意之餘，更能豐富視覺享受。</p>';
                    vm.displaySubText = '<h6>周邊景點：</h6><p><a href="https://tour.ntpc.gov.tw/zh-tw/Attraction/Detail?wnd_id=60&id=109613">碧潭風景區</a>、<a href="https://tour.ntpc.gov.tw/zh-tw/Attraction/Detail?wnd_id=60&id=109987">新店老街</a></p>';
                    break;
                case 10:
                    vm.displayTitle = '鶯歌｜鶯歌石步道、孫龍步道';
                    vm.displayImg = [require('./assets/10-1.jpg'), require('./assets/10-2.jpg'), require('./assets/10-3.jpg'), require('./assets/10-4.jpg')];
                    vm.imgResouce = '照片來源：新北市觀光旅遊局《新北登山小旅行》';
                    vm.imgdirection = [0,0,0,0];
                    vm.picText = ['二坑隧道', '孫龍步道', '孫龍步道起點宏德宮(孫臏廟)', '鶯歌石步道'];
                    vm.displayText = '<p>海拔標高約243公尺，全長約2.9公里，石孫龍得名由來十分特別，是台灣第一間供奉孫臏的宮廟，孫臏是創「孫子兵法」孫武的後代，後人尊稱為「兵學亞聖」，在台灣歷史發展期間，石孫龍步道曾是一處煤礦運輸道，如今產業逝去，但歷史也豐富了步道色彩。</p><p>步道拾階而上，穿越小拱橋，途經岩壁上有天然的石窟，內有神像和日據時代的石碑，風吹徐徐、撫過山林綠葉，陽光穿透，照映人文的價值、也體現生態的可貴，處處有驚奇交錯。帶著怡然自如的美好心情，走過這段珍貴的路程，緩步下階，進入鶯歌小鎮，又是一處景致。</p>';
                    vm.displaySubText = '<h6>周邊景點：</h6><p><a href="https://tour.ntpc.gov.tw/zh-tw/Attraction/Detail?wnd_id=60&id=110661">鶯歌老街</a>、<a href="https://tour.ntpc.gov.tw/zh-tw/Attraction/Detail?wnd_id=60&id=109616">鶯歌陶瓷博物館</a></p>';
                    break;
                case 11:
                    vm.displayTitle = '汐止｜大尖山步道';
                    vm.displayImg = [require('./assets/11-1.jpg'), require('./assets/11-2.jpg'), require('./assets/11-3.jpg'), require('./assets/11-4.jpg')];
                    vm.imgResouce = '照片來源：新北市觀光旅遊局《新北登山小旅行》';
                    vm.imgdirection = [0,0,1,1];
                    vm.picText = ['大尖山', '大尖山的展望視野', '天秀宮往秀峰瀑布途中的林蔭步道', '秀峰瀑布'];
                    vm.displayText = '<p>海拔標高約460公尺，全長約2.6公里。位於汐止的大尖山如其名，因山形尖峻而得名，為台灣小百岳之一，同時大尖山步道也是知名的櫻花步道，從山頂眺望而下，一覽無遺基隆到台北盆地的都會美景。</p><p>進入步道前途經天秀宮，其廣場是在地居民休閒交誼、山友歇腳的好去處，此宮供奉關聖帝君，假日香客更是絡繹不絕，步入古道，沿途青苔老石，禪意樸質，蜿蜒著茄苳溪，溪聲潺潺入耳，那五層樓高的茄苳瀑布，洗滌日常煩憂，眼前是壯觀瀑布、身邊是翠綠山林，環繞般的視覺享受，沈澱心靈，是古道帶給山友們最大的禮物。</p>';
                    vm.displaySubText = '<h6>周邊景點：</h6><p><a href="https://tour.ntpc.gov.tw/zh-tw/Attraction/Detail?wnd_id=60&id=110883">汐止老街</a>、<a href="https://tour.ntpc.gov.tw/zh-tw/Attraction/Detail?wnd_id=60&id=402215">濟德宮</a>、古厝</p>';
                    break;
            }
        },
    }
};
</script>
