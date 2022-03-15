<?php
/*Ushbu kod: Xurrambek Obiddinov (https://t.me/Diyorbekahmadjonov) tomonidan yozilgan. Iltimos, mualliflik huquqi hurmat qilinsin!*/
ob_start();
define("Diyorbekahmadjonov","5179650373:AAFXnio6Erz04TUxfVvRzkpnbTSXpMx-d_M");
$admin = "1393587687";
$botname = "@jhjdhfddgdgfdgfdjgdjgdjfjjbot";
$arays = array($arays,$admin);

function addstat($id){
    $check = file_get_contents("Diyorbekahmadjonov.bot");
    $rd = explode("\n",$check);
    if(!in_array($id,$rd)){
        file_put_contents("Diyorbekahmadjonov.bot","\n".$id,FILE_APPEND);
    }
}

function banstat($id){
    $check = file_get_contents("Diyorbekahmadjonov.ban");
    $rd = explode("\n",$check);
    if(!in_array($id,$rd)){
        file_put_contents("Diyorbekahmadjonov.ban","\n".$id,FILE_APPEND);
    }
}

function step($id,$value){
file_put_contents("Diyorbekahmadjonov/$id.step","$value");
}

function stepbot($id,$value){
file_put_contents("Diyorbekahmadjonovbot/$id.step","$value");
}

function typing($chatid){ 
return Diyorbekahmadjonov("sendChatAction",[
"chat_id"=>$chatid,
"action"=>"typing",
]);
}

function joinchat($id){
     global $message_id,$referalsum,$firstname;
     $ret = Diyorbekahmadjonov("getChatMember",[
         "chat_id"=>"-1001443915790",
         "user_id"=>$id,
         ]);
$stat = $ret->result->status;
$rets = Diyorbekahmadjonov("getChatMember",[
         "chat_id"=>"-1001562645446",
         "user_id"=>$id,
         ]);
$stats = $rets->result->status;
$retus = Diyorbekahmadjonov("getChatMember",[
         "chat_id"=>"-1001582073156",
         "user_id"=>$id,
         ]);
$status = $retus->result->status;
         if((($stat=="creator" or $stat=="administrator" or $stat=="member") and ($stats=="creator" or $stats=="administrator" or $stats=="member") and ($status=="creator" or $status=="administrator" or $status=="member"))){
      return true;
         }else{
     Diyorbekahmadjonov("sendMessage",[
         "chat_id"=>$id,
         "text"=>"<b>Quyidagi kanallarimizga obuna boʻling. Botni keyin toʻliq ishlatishingiz mumkin!</b>",
         "parse_mode"=>"html",
         "reply_to_message_id"=>$message_id,
"disable_web_page_preview"=>true,
"reply_markup"=>json_encode([
"inline_keyboard"=>[
[["text"=>"💸 HOMIY KANAL 💸","url"=>"https://t.me/TgFOYDALi_BOTLAR"],],
[["text"=>"💸 HOMIY KANAL💸","url"=>"https://t.me/joinchat/vHIA_h6LaGc3N2Yy"],],
[["text"=>"💰 TOLOV KANALI 💰","url"=>"https://t.me/TgShartBor"],],
[["text"=>"✅ Tasdiqlash","callback_data"=>"result"],],
]
]),
]);  
sleep(2);
     if(file_exists("Diyorbekahmadjonov/".$id.".referalid")){
           $file =  file_get_contents("Diyorbekahmadjonov/".$id.".referalid");
           $get =  file_get_contents("Diyorbekahmadjonov/".$id.".channel");
           if($get=="true"){
            file_put_contents("Diyorbekahmadjonov/".$id.".channel","failed");
            $minimal = $referalsum / 2;
            $user = file_get_contents("Diyorbekahmadjonov/".$file.".Pul");
            $user = $user - $minimal;
            file_put_contents("Diyorbekahmadjonov/".$file.".Pul","$user");
             Diyorbekahmadjonov("sendMessage",[
             "chat_id"=>$file,
             "text"=>"<b>Sizning do'stingiz</b>, <a href='tg://user?id=".$id."'>".$firstname."</a> <b>bizning kanallarimizdan chiqib ketgani uchun sizga ".$minimal." so'm jarima berildi.</b>",
             "parse_mode"=>"html",
             "reply_markup"=>$menu,
             ]);
           }
         }  
return false;
}
}

function phonenumber($id){
     $phonenumber = file_get_contents("Diyorbekahmadjonov/$id.contact");
      if($phonenumber==true){
      return true;
         }else{
     stepbot($id,"request_contact");
     Diyorbekahmadjonov("sendPhoto",[
    "chat_id"=>$id,
"photo"=>"https://t.me/BotRasmlari/2",
    "caption"=>"<b>Salom, hurmatli foydalanuvchi!</b>\n<b>Pul ishlash ishonchli bo'lishi uchun, pastdagi «📲 Telefon raqamni yuborish» tugmasini bosing:</b>",
    "parse_mode"=>"html",
    "reply_markup"=>json_encode([
      "resize_keyboard"=>true,
      "one_time_keyboard"=>true,
      "keyboard"=>[
        [["text"=>"📲 Telefon raqamni yuborish","request_contact"=>true],],
]
]),
]);  
return false;
}
}

function reyting(){
    $text = "🏆 <b>TOP 20 ta eng koʻp Pul ishlagan foydalanuvchilar:</b>\n\n";
    $daten = [];
    $rev = [];
    $fayllar = glob("./Diyorbekahmadjonov/*.*");
    foreach($fayllar as $file){
        if(mb_stripos($file,".Pul")!==false){
        $value = file_get_contents($file);
        $id = str_replace(["./Diyorbekahmadjonov/",".Pul"],["",""],$file);
        $daten[$value] = $id;
        $rev[$id] = $value;
        }
        echo $file;
    }

    asort($rev);
    $reversed = array_reverse($rev);
    for($i=0;$i<20;$i+=1){
        $order = $i+1;
        $id = $daten["$reversed[$i]"];
        $text.= "<b>{$order}</b>. <a href='tg://user?id={$id}'>{$id}</a> - "."<code>".$reversed[$i]."</code>"." <b>soʻm</b>"."\n";
    }
    return $text;
}

function Diyorbekahmadjonov($method,$datas=[]){
    $url = "https://api.telegram.org/bot".Diyorbekahmadjonov."/".$method;
    $ch = curl_init();
    curl_setopt($ch,CURLOPT_URL,$url);
    curl_setopt($ch,CURLOPT_RETURNTRANSFER,true);
    curl_setopt($ch,CURLOPT_POSTFIELDS,$datas);
    $res = curl_exec($ch);
    if(curl_error($ch)){
        var_dump(curl_error($ch));
    }else{
        return json_decode($res);
    }
}

$update = json_decode(file_get_contents('php://input'));
$message = $update->message;
$callbackdata = $update->callback_query->data;
$chatid = $message->chat->id;
$chat_id = $update->callback_query->message->chat->id;
$messageid = $message->message_id;
$id = $update->callback_query->id;
$fromid = $message->from->id;
$from_id = $update->callback_query->from->id;
$firstname = $message->from->first_name;
$first_name = $update->callback_query->from->first_name;
$lastname = $message->from->last_name;
$message_id = $update->callback_query->message->message_id;
$text = $message->text;
$contact = $message->contact;
$contactid = $contact->user_id;
$contactuser = $contact->username;
$contactname = $contact->first_name;
$phonenumber = $contact->phone_number;
$messagereply = $message->reply_to_message->message_id;
$user = $message->from->username;
$userid = $update->callback_query->from->username;
$query = $update->inline_query->query;
$inlineid = $update->inline_query->from->id;
$messagereply = $message->reply_to_message->message_id;
$soat = date("H:i:s",strtotime("2 hour")); 
$sana = date("d-M Y",strtotime("2 hour"));
$resultid = file_get_contents("Diyorbekahmadjonov.bot");
$ban = file_get_contents("Diyorbekahmadjonov/$chatid.ban");
$banid = file_get_contents("Diyorbekahmadjonov/$chat_id.ban");
$sabab = file_get_contents("Diyorbekahmadjonov/$chat_id.sabab");
$contact = file_get_contents("Diyorbekahmadjonov/$chatid.contact");
$minimalsumma = file_get_contents("Diyorbekahmadjonov/minimal.sum");
$sum = file_get_contents("Diyorbekahmadjonov/$chatid.Pul");
$sumid = file_get_contents("Diyorbekahmadjonov/$chat_id.Pul");
$jami = file_get_contents("Diyorbekahmadjonov/summa.text");
$referal = file_get_contents("Diyorbekahmadjonov/$chatid.referal");
$referalcallback = file_get_contents("Diyorbekahmadjonov/$chat_id.referal");
$click = file_get_contents("Diyorbekahmadjonov/$chatid.karta");
$paynet = file_get_contents("Diyorbekahmadjonov/$chatid.paynet");
$click = file_get_contents("Diyorbekahmadjonov/$chatid.click");
$referalsum = file_get_contents("Diyorbekahmadjonov/referal.sum");
if(file_get_contents("Diyorbekahmadjonov/minimal.sum")){
}else{    file_put_contents("Diyorbekahmadjonov/minimal.sum","10000");
}
if(file_get_contents("Diyorbekahmadjonov/$chatid.referal")){
}else{    file_put_contents("Diyorbekahmadjonov/$chatid.referal","0");
}
if(file_get_contents("Diyorbekahmadjonov/$chat_id.referal")){
}else{    file_put_contents("Diyorbekahmadjonov/$chat_id.referal","0");
}
if(file_get_contents("Diyorbekahmadjonov/summa.text")){
}else{    file_put_contents("Diyorbekahmadjonov/summa.text","0");
}
if(file_get_contents("Diyorbekahmadjonov/referal.sum")){
}else{    file_put_contents("Diyorbekahmadjonov/referal.sum","0");
}
if(file_get_contents("Diyorbekahmadjonov/$chatid.Pul")){
}else{    file_put_contents("Diyorbekahmadjonov/$chatid.Pul","0");
}
if(file_get_contents("Diyorbekahmadjonov/$chat_id.Pul")){
}else{    file_put_contents("Diyorbekahmadjonov/$chat_id.Pul","0");
}
if(file_get_contents("Diyorbekahmadjonov/$chat_id.sabab")){
}else{    file_put_contents("Diyorbekahmadjonov/$chat_id.sabab","Botdan faqat O'zbekiston fuqarolari foydalanishi mumkin! Uqdingmi!!!");
}
$step = file_get_contents("Diyorbekahmadjonov/$chatid.step");
$step = file_get_contents("Diyorbekahmadjonovbot/$chatid.step");
mkdir("Diyorbekahmadjonov");
mkdir("Diyorbekahmadjonovbot");
if(!is_dir("Diyorbekahmadjonov")){
  mkdir("Diyorbekahmadjonov");
}

$menu = json_encode([
"resize_keyboard"=>true,
    "keyboard"=>[
[["text"=>"♻️ Pul ishlash"],["text"=>"🏆 Reyting"],],
[["text"=>"💰 Hisobim"],["text"=>"🗒 Qo‘llanma"],],
[["text"=>"💌 Biz bilan aloqa"],],
]
]);

$panel = json_encode([
"resize_keyboard"=>true,
    "keyboard"=>[
[["text"=>"🗣 Userlarga xabar yuborish"],],
[["text"=>"💳 Hisob tekshirish"],["text"=>"💰 Hisob toʻldirish"],],
[["text"=>"👥 Referal narxini o'zgartirish"],],
[["text"=>"✅ Bandan olish"],["text"=>"🚫 Ban berish"],],
[["text"=>"📤 Minimal Pul yechish"],],
[["text"=>"⬅️ Ortga"],],
]
]);

$back = json_encode([
 "one_time_keyboard"=>true,
"resize_keyboard"=>true,
    "keyboard"=>[
[["text"=>"⬅️ Ortga"],],
]
]);

if(($step=="request_contact") and ($ban==false) and (isset($phonenumber))){
$phonenumber = str_replace("+","","$phonenumber");
if(joinchat($fromid)=="true"){
if((strlen($phonenumber)==12) and (stripos($phonenumber,"9989")!==false)){
if($contactid==$chatid){
addstat($fromid);
if($user){
$username = "@$user";
}else{
$username = "$firstname";
}
if(file_exists("Diyorbekahmadjonov/".$fromid.".referalid")){
$referalid = file_get_contents("Diyorbekahmadjonov/".$fromid.".referalid"); 
$channel = file_get_contents("Diyorbekahmadjonov/".$fromid.".channel");
$conts = file_get_contents("Diyorbekahmadjonov/".$fromid.".login");
if($channel=="true" and $conts=="false"){
if(joinchat($referalid)=="true"){
file_put_contents("Diyorbekahmadjonov/".$fromid.".login","true");
Diyorbekahmadjonov("deleteMessage",[
"chat_id"=>$chat_id,
"message_id"=>$message_id,
]);
$user = file_get_contents("Diyorbekahmadjonov/".$referalid.".Pul");
$referalsum = $referalsum / 2;
$user = $user + $referalsum;
file_put_contents("Diyorbekahmadjonov/".$referalid.".Pul","$user");
$firstname = str_replace(["<",">","/"],["","",""],$firstname);
Diyorbekahmadjonov("sendMessage",[
"chat_id"=>$referalid,
"text"=>"<b>👏 Tabriklaymiz! Sizni do'stingiz</b> <a href='tg://user?id=$fromid'>$firstname</a> <b>botimizdan ro'yxatdan o'tdi va sizga $referalsum so'm taqdim etildi.</b>",
"parse_mode"=>"html",
"reply_markup"=>$menu,
]);
}
}
}
$reply = Diyorbekahmadjonov("sendMessage",[
"chat_id"=>$fromid,
"text"=>"<b>Quyidagi havolani doʻstlaringizga tarqatib Pul ishlang!</b> 👇",
"parse_mode"=>"html",
"reply_markup"=>$menu,
])->result->message_id;
Diyorbekahmadjonov("sendMessage",[
"chat_id"=>$fromid,
"text"=>"✅ <b>@TgShartBor tanlovining rasmiy boti</b> 🤖\n\n🎈 $username do'stingizdan unikal havola-taklifnoma.\n\n👇 Boshlash Pulhun bosing:\nhttps://t.me/$botname?start=$fromid",
"parse_mode"=>"html",
"reply_to_message_id"=>$reply,
"disable_web_page_preview"=>true,
"reply_markup"=>json_encode([
"inline_keyboard"=>[
[["text"=>"↗️ Doʻstlarga yuborish","switch_inline_query"=>$fromid],],
]
]),
]);
unlink("Diyorbekahmadjonovbot/$chatid.step");
file_put_contents("Diyorbekahmadjonov/$chatid.contact","$phonenumber");
}else{
  addstat($chatid);
  Diyorbekahmadjonov("sendMessage",[
    "chat_id"=>$chatid,
    "text"=>"<b>Faqat o'zingizni kontaktingizni yuboring:</b>",
    "parse_mode"=>"html",
    "reply_markup"=>json_encode([
      "resize_keyboard"=>true,
      "one_time_keyboard"=>true,
      "keyboard"=>[
        [["text"=>"📲 Telefon raqamni yuborish","request_contact"=>true],],
]
]),
]);
}
}else{
  banstat($chatid);
  Diyorbekahmadjonov("sendMessage",[
    "chat_id"=>$chatid,
    "text"=>"<b>Kechirasiz! Botdan faqat O'zbekiston fuqarolari foydalanishi mumkin!</b>",
    "parse_mode"=>"html",
    "reply_to_message_id"=>$messageid,
    "reply_markup"=>json_encode([
    "remove_keyboard"=>true,
    ]),
  ]);
unlink("Diyorbekahmadjonovbot/$chatid.step");
file_put_contents("Diyorbekahmadjonov/$chatid.ban","ban");
}
}
}

if($text=="/admin" and $chatid==$admin){
typing($chatid);
Diyorbekahmadjonov('sendMessage',[
"chat_id"=>$chatid,
"text"=>"<b>Salom ❤Xojiakbar❤, Siz bot administratorisiz. Kerakli boʻlimni tanlang 😘Men sizni sevaman😘:</b>",
"parse_mode"=>"html",
"reply_markup"=>$panel,
]);
}

if($text=="🗣 Userlarga xabar yuborish" and $chatid==$admin){
typing($chatid);
stepbot($chatid,"send_post");
      Diyorbekahmadjonov("sendMessage",[
      "chat_id"=>$chatid,
      "text"=>"<b>Rasmli xabar matnini kiriting. Xabar turi markdown:</b>",
      "parse_mode"=>"html",
          "reply_markup"=>$panel,
          ]);
            }

     if($step=="send_post" and $chatid==$admin){
        $file_id = $message->photo[0]->file_id;
        $caption = $message->caption;
                $ok = Diyorbekahmadjonov("sendPhoto",[
                  "chat_id"=>$chatid,
                  "photo"=>$file_id,
                  "caption"=>$caption,
                  "parse_mode"=>"markdown",
                ]);
                if($ok->ok){
                  Diyorbekahmadjonov("sendPhoto",[
                    "chat_id"=>$chatid,
                    "photo"=>$file_id,
                      "caption"=>"$caption\n\nYaxshi, rasmni qabul qildim!\nEndi tugmani na‘muna bo'yicha joylang.\n
<pre>[XOJIAKBAR+https://t.me/XOJIAKBAR_KAMOLOV]\n[Yangiliklar+https://t.me/XOJIAKBAR_KAMOLOV]</pre>",
"parse_mode"=>"html",
                      "disable_web_page_preview"=>true,
                    ]);
             file_put_contents("Diyorbekahmadjonovbot/$chatid.text","$file_id{set}$caption");
             stepbot($chatid,"xabar_tugma");
         }
     }
     
    if($step=="xabar_tugma" and $chatid==$admin){
      $xabar = Diyorbekahmadjonov("sendMessage",[
        "chat_id"=>$chatid,
        "text"=>"Connections...",
      ])->result->message_id;
      Diyorbekahmadjonov("deleteMessage",[
        "chat_id"=>$chat_id,
        "message_id"=>$xabar,
      ]);
   $usertext = file_get_contents("Diyorbekahmadjonovbot/$chatid.text");
   $fileid = explode("{set}",$usertext);
   $file_id = $fileid[0];
   $caption = $fileid[1];
       preg_match_all("|\[(.*)\]|U",$text,$ouvt);
$keyboard = [];
foreach($ouvt[1] as $ouut){
$ot = explode("+",$ouut);
array_push($keyboard,[["url"=>"$ot[1]", "text"=>"$ot[0]"],]);
}
$ok = Diyorbekahmadjonov("sendPhoto",[
"chat_id"=>$chatid,
"photo"=>$file_id,
"caption"=>"Sizning rasmingiz ko‘rinishi:\n\n".$caption,
"parse_mode"=>"html",
"reply_markup"=>json_encode(
["inline_keyboard"=>
$keyboard
]),
]);
if($ok->ok){
$userlar = file_get_contents("Diyorbekahmadjonov.bot");
$count = substr_count($userlar,"\n");
$count_member = count(file("Diyorbekahmadjonov.bot"))-1;
  $ids = explode("\n",$userlar);
  foreach ($ids as $line => $id) {
    $clear = Diyorbekahmadjonov("sendPhoto",[
"chat_id"=>$id,
"photo"=>$file_id,
"caption"=>$caption,
"parse_mode"=>"markdown",
"disable_web_page_preview"=>true,
"reply_markup"=>json_encode(
["inline_keyboard"=>
$keyboard
]),
]);
unlink("Diyorbekahmadjonovbot/$chatid.step");
}

if($clear){
$userlar = file_get_contents("Diyorbekahmadjonov.bot");
$count = substr_count($userlar,"\n");
$count_member = count(file("Diyorbekahmadjonov.bot"))-1;
  Diyorbekahmadjonov("sendMessage",[
    "chat_id"=>$chatid,
    "text"=>"Xabar <b>$count_member</b> userlarga yuborildi!",
    "parse_mode"=>"html",
  ]);
}
}else{
  Diyorbekahmadjonov("sendMessage",[
    "chat_id"=>$chatid,
    "text"=>"Tugmani kiritishda xato bor. Iltimos, qaytadan yuboring:",
  ]);
unlink("Diyorbekahmadjonovbot/$chatid.step");  
}
}

if($text=="💳 Hisob tekshirish" and $chatid==$admin){
typing($chatid);
stepbot($chatid,"result");
Diyorbekahmadjonov("sendMessage",[
"chat_id"=>$admin,
"text"=>"<b>Foydalanuvchini ID raqamini kiriting:</b>",
"parse_mode"=>"html",
"reply_markup"=>$panel,
]);
}

if($step=="result" and $chatid==$admin){
typing($chatid);
if($text=="🗣 Userlarga xabar yuborish" or $text=="👥 Referal narxini o'zgartirish" or $text=="💳 Hisob tekshirish" or $text=="💰 Hisob toʻldirish" or $text=="✅ Bandan olish" or $text=="🚫 Ban berish" or $text=="📤 Minimal Pul yechish" or $text=="⬅️ Ortga"){
}else{
$sum = file_get_contents("Diyorbekahmadjonov/$text.Pul");
$referal = file_get_contents("Diyorbekahmadjonov/$text.referal");
$raqam = file_get_contents("Diyorbekahmadjonov/$text.contact");
Diyorbekahmadjonov("sendMessage",[
"chat_id"=>$admin,
"text"=>"<b>Foydalanuvchi hisobi:</b> <code>$sum</code>\n<b>Foydalanuvchi referali:</b> <code>$referal</code>\n<b>Foydalanuvchi raqami:</b> <code>$raqam</code>",
"parse_mode"=>"html",
"reply_markup"=>$panel,
]);
}
}

if($text=="💰 Hisob toʻldirish" and $chatid==$admin){
typing($chatid);
stepbot($chatid,"coin");
Diyorbekahmadjonov("sendMessage",[
"chat_id"=>$admin,
"text"=>"<b>Foydalanuvchi hisobini necha Pulga toʻldirmoqchisiz:</b>",
"parse_mode"=>"html",
"reply_markup"=>$panel,
]);
}

if($step=="coin" and $chatid==$admin){
typing($chatid);
file_put_contents("Diyorbekahmadjonov/$chatid.coin",$text);
if($text=="🗣 Userlarga xabar yuborish" or $text=="👥 Referal narxini o'zgartirish" or $text=="💳 Hisob tekshirish" or $text=="💰 Hisob toʻldirish" or $text=="✅ Bandan olish" or $text=="🚫 Ban berish" or $text=="📤 Minimal Pul yechish" or $text=="⬅️ Ortga"){
}else{
stepbot($chatid,"pay");
Diyorbekahmadjonov("sendMessage",[
"chat_id"=>$admin,
"text"=>"<b>Foydalanuvchi ID raqamini kiriting:</b>",
"parse_mode"=>"html",
"reply_markup"=>$panel,
]);
}
}

if($step=="pay" and $chatid==$admin){
typing($chatid);
if($text=="🗣 Userlarga xabar yuborish" or $text=="👥 Referal narxini o'zgartirish" or $text=="💳 Hisob tekshirish" or $text=="💰 Hisob toʻldirish" or $text=="✅ Bandan olish" or $text=="🚫 Ban berish" or $text=="📤 Minimal Pul yechish" or $text=="⬅️ Ortga"){
}else{
$summa = file_get_contents("Diyorbekahmadjonov/$chatid.coin");
$sum =  file_get_contents("Diyorbekahmadjonov/$text.Pul");
$jami = $sum + $summa;
file_put_contents("Diyorbekahmadjonov/$text.Pul","$jami");
Diyorbekahmadjonov("sendMessage",[
   "chat_id"=>$text,
          "text"=>"💰 Hisobingiz: $summa so'mga to'ldirildi!\nHozirgi hisobingiz: $jami",
]);
Diyorbekahmadjonov("sendMessage",[
"chat_id"=>$admin,
"text"=>"<b>Foydalanuvchi balansi toʻldirildi!</b>",
"parse_mode"=>"html",
"reply_markup"=>$panel,
]);
unlink("Diyorbekahmadjonovbot/$chatid.step");
}
}

if($text=="👥 Referal narxini o'zgartirish" and $chatid==$admin){
typing($chatid);
stepbot($chatid,"referal");
Diyorbekahmadjonov("sendMessage",[
"chat_id"=>$admin,
"text"=>"<b>Referal narxini kiriting:</b>",
"parse_mode"=>"html",
"reply_markup"=>$panel,
]);
}

if($step=="referal" and $chatid==$admin){
typing($chatid);
if($text=="🗣 Userlarga xabar yuborish" or $text=="👥 Referal narxini o'zgartirish" or $text=="💳 Hisob tekshirish" or $text=="💰 Hisob toʻldirish" or $text=="✅ Bandan olish" or $text=="🚫 Ban berish" or $text=="📤 Minimal Pul yechish" or $text=="⬅️ Ortga"){
}else{
file_put_contents("Diyorbekahmadjonov/referal.sum","$text");
Diyorbekahmadjonov("sendMessage",[
"chat_id"=>$admin,
"text"=>"<b>Referal taklif qilish narxi: $text so'mga o'zgardi!</b>",
"parse_mode"=>"html",
"reply_markup"=>$panel,
]);
unlink("Diyorbekahmadjonovbot/$chatid.step");
}
}

if($text=="✅ Bandan olish" and $chatid==$admin){
stepbot($chatid,"unban");
Diyorbekahmadjonov("sendMessage",[
"chat_id"=>$admin,
"text"=>"<b>Foydalanuvchini ID raqamini kiriting:</b>",
"parse_mode"=>"html",
"reply_markup"=>$panel,
]);
}

if($step=="unban" and $chatid==$admin){
unlink("Diyorbekahmadjonov/$text.ban");
if($text=="🗣 Userlarga xabar yuborish" or $text=="👥 Referal narxini o'zgartirish" or $text=="💳 Hisob tekshirish" or $text=="💰 Hisob toʻldirish" or $text=="✅ Bandan olish" or $text=="🚫 Ban berish" or $text=="📤 Minimal Pul yechish" or $text=="⬅️ Ortga"){
}else{
Diyorbekahmadjonov("sendMessage",[
"chat_id"=>$chatid,
"text"=>"<a href='tg://user?id=$text'>Foydalanuvchi</a> <b>bandan olindi!</b>",
"parse_mode"=>"html",
"reply_markup"=>$panel,
]);
unlink("Diyorbekahmadjonovbot/$chatid.step");
}
}

if($text=="🚫 Ban berish" and $chatid==$admin){
stepbot($chatid,"sabab");
Diyorbekahmadjonov("sendMessage",[
"chat_id"=>$admin,
"text"=>"<b>Foydalanuvchini nima sababdan ban qilmoqchisiz:</b>",
"parse_mode"=>"html",
"reply_markup"=>$panel,
]);
}

if($step=="sabab" and $chatid==$admin){
file_put_contents("Diyorbekahmadjonov/$chatid.sabab","$text");
Diyorbekahmadjonov("sendMessage",[
"chat_id"=>$admin,
"text"=>"<b>Foydalanuvchini ID raqamini kiriting:</b>",
"parse_mode"=>"html",
"reply_markup"=>$panel,
]);
stepbot($chatid,"ban");
}

if($step=="ban" and $chatid==$admin){
banstat($text);
$sabab = file_get_contents("Diyorbekahmadjonov/$chatid.sabab");
file_put_contents("Diyorbekahmadjonov/$text.sabab","$sabab");
file_put_contents("Diyorbekahmadjonov/$text.ban","ban");
if($text=="🗣 Userlarga xabar yuborish" or $text=="👥 Referal narxini o'zgartirish" or $text=="💳 Hisob tekshirish" or $text=="💰 Hisob toʻldirish" or $text=="✅ Bandan olish" or $text=="🚫 Ban berish" or $text=="📤 Minimal Pul yechish" or $text=="⬅️ Ortga"){
}else{
Diyorbekahmadjonov("sendMessage",[
"chat_id"=>$chatid,
"text"=>"<a href='tg://user?id=$text'>Foydalanuvchi</a> <b>banlandi!</b>",
"parse_mode"=>"html",
"reply_markup"=>$panel,
]);
unlink("Diyorbekahmadjonovbot/$chatid.step");
Diyorbekahmadjonov("sendMessage",[
"chat_id"=>$text,
"text"=>"<b>Hurmatli foydalanuvchi!</b>\n<b>Siz botdan banlandingiz. Shuning Pulhun botni ishlata olmaysiz!</b>",
"parse_mode"=>"html",
"reply_markup"=>json_encode([
"inline_keyboard"=>[
[["text"=>"📃 Batafsil maʼlumot","callback_data"=>"sabab"],],
]
]),
]);
}
}

if($text=="📤 Minimal Pul yechish" and $chatid==$admin){
typing($chatid);
stepbot($chatid,"minimalsumma");
Diyorbekahmadjonov("sendMessage",[
"chat_id"=>$admin,
"text"=>"<b>Minimal Pul yechish narxini kiriting:</b>",
"parse_mode"=>"html",
"reply_markup"=>$panel,
]);
}

if($step=="minimalsumma" and $chatid==$admin){
typing($chatid);
if($text=="🗣 Userlarga xabar yuborish" or $text=="👥 Referal narxini o'zgartirish" or $text=="💳 Hisob tekshirish" or $text=="💰 Hisob toʻldirish" or $text=="✅ Bandan olish" or $text=="🚫 Ban berish" or $text=="📤 Minimal Pul yechish" or $text=="⬅️ Ortga"){
}else{
file_put_contents("Diyorbekahmadjonov/minimal.sum","$text");
Diyorbekahmadjonov("sendMessage",[
"chat_id"=>$admin,
"text"=>"<b>Minimal Pul yechish narxi: $text so'mga o'zgardi!</b>",
"parse_mode"=>"html",
"reply_markup"=>$panel,
]);
unlink("Diyorbekahmadjonovbot/$chatid.step");
}
}

if($callbackdata=="back" and $banid==false){
if((joinchat($from_id)=="true") and (phonenumber($from_id)=="true") and ($banid==false)){
Diyorbekahmadjonov("deleteMessage",[
"chat_id"=>$chat_id,
"message_id"=>$message_id,
]);
Diyorbekahmadjonov("sendMessage",[
"chat_id"=>$chat_id,
"text"=>"<b>Kerakli boʻlimni tanlang</b> 👇",
"parse_mode"=>"html",
"reply_markup"=>$menu,
]);
}
}

if($text=="♻️ Pul ishlash" and $ban==false){
if((joinchat($fromid)=="true") and (phonenumber($fromid)=="true") and ($ban==false)){
if($user){
$username = "@$user";
}else{
$username = "$firstname";
}
Diyorbekahmadjonov("sendPhoto",[
    "chat_id"=>$chatid,
"photo"=>"https://t.me/TgFOYDALi_BOTLAR/307",
    "caption"=>"✅ <b>@TgShartBor tanlovining rasmiy boti</b> 🤖\n\n🎈 $username do'stingizdan unikal havola-taklifnoma.\n\n👇 Boshlash uchun bosing:
https://t.me/$botname?start=$chatid",
"parse_mode"=>"html",
"disable_web_page_preview"=>true,
"reply_markup"=>json_encode([
"inline_keyboard"=>[
[["text"=>"↗️ Doʻstlarga yuborish","switch_inline_query"=>$chatid],],
]
]),
]);
}
}

if($text=="💰 Hisobim" and $ban==false){
if((joinchat($fromid)=="true") and (phonenumber($fromid)=="true") and ($ban==false)){
Diyorbekahmadjonov('sendMessage',[
"chat_id"=>$chatid,
"text"=>"<b>Sizning hisobingiz:</b> <code>$sum</code>\n\n<b>Siz botga taklif qilgan a'zolar soni:</b> <code>$referal</code>\n\n<b>Bot toʻlab bergan jami summa:</b> <code>$jami</code>\n\n<b>Pul yechib olish Pulhun minimal summa:</b> <code>$minimalsumma</code> <b>soʻm</b>",
"parse_mode"=>"html",
"reply_markup"=>json_encode([
"inline_keyboard"=>[
[["text"=>"📤 Pul yechish","callback_data"=>"prodPultion"],],
]
]),
]);
}
}

if($text=="🏆 Reyting" and $ban==false){
if((joinchat($fromid)=="true") and (phonenumber($fromid)=="true") and ($ban==false)){
$reyting = reyting();
Diyorbekahmadjonov("sendMessage",[
"chat_id"=>$chatid,
"text"=>"$reyting",
"parse_mode"=>"html",
"reply_markup"=>$menu,
]);
}
}

if($text=="⬅️ Ortga" and $ban==false){
if((joinchat($fromid)=="true") and (phonenumber($fromid)=="true") and ($ban==false)){
addstat($chatid);
Diyorbekahmadjonov("sendMessage",[
"chat_id"=>$chatid,
"text"=>"<b>Kerakli boʻlimni tanlang</b> 👇",
"parse_mode"=>"html",
"reply_markup"=>$menu,
]);
unlink("Diyorbekahmadjonov/$chatid.step");
unlink("Diyorbekahmadjonovbot/$chatid.step");
}
}

if((stripos($text,"/start")!==false) && ($ban==false)){
if((joinchat($fromid)=="true") and (phonenumber($fromid)=="true") and ($ban==false)){
addstat($fromid);
if($user){
$username = "@$user";
}else{
$username = "$firstname";
}
$reply = Diyorbekahmadjonov("sendMessage",[
"chat_id"=>$fromid,
"text"=>"<b>Quyidagi havolani doʻstlaringizga tarqatib Pul ishlang!</b> 👇",
"parse_mode"=>"html",
"reply_markup"=>$menu,
])->result->message_id;
Diyorbekahmadjonov("sendMessage",[
"chat_id"=>$fromid,
"text"=>"✅ <b>@TgShartBor tanlovining rasmiy boti</b> 🤖\n\n🎈 $username do'stingizdan unikal havola-taklifnoma.\n\n👇 Boshlash uchun bosing:\nhttps://t.me/$botname?start=$fromid",
"parse_mode"=>"html",
"reply_to_message_id"=>$reply,
"disable_web_page_preview"=>true,
"reply_markup"=>json_encode([
"inline_keyboard"=>[
[["text"=>"↗️ Doʻstlarga yuborish","switch_inline_query"=>$fromid],],
]
]),
]);
}
}

if((stripos($text,"/start")!==false) && ($ban==false)){
$public = explode("*",$text);
$refid = explode(" ",$text);
$refid = $refid[1];
if(strlen($refid)>0){
$idref = "Diyorbekahmadjonov/$refid.id";
$idrefs = file_get_contents($idref);
$userlar = file_get_contents("Diyorbekahmadjonov.bot");
$explode = explode("\n",$userlar);
if(!in_array($chatid,$explode)){
file_put_contents("Diyorbekahmadjonov.bot","\n".$chatid,FILE_APPEND);
}
if($refid==$chatid and $ban==false){
      Diyorbekahmadjonov("sendMessage",[
      "chat_id"=>$chatid,
      "text"=>"☝️ <b>Hurmatli foydalanuvchi!</b>\n<b>Botga o'zingizni taklif qila olmaysiz!</b>",
      "parse_mode"=>"html",
      "reply_to_message_id"=>$messageid,
      ]);
      }else{
    if((stripos($userlar,"$chatid")!==false) and ($ban==false)){
      Diyorbekahmadjonov("sendMessage",[
      "chat_id"=>$chatid,
      "text"=>"<b>Hurmatli foydalanuvchi!</b>\n<b>Siz do'stingizga referal bo'la olmaysiz, agar ushbu holat yana takrorlansa, siz botdan blocklanishingiz mumkin!</b>",
"parse_mode"=>"html",
"reply_to_message_id"=>$messageid,
]);
}else{
$id = "$chatid\n";
$handle = fopen("$idref","a+");
fwrite($handle,$id);
fclose($handle);
file_put_contents("Diyorbekahmadjonov/$fromid.referalid","$refid");
file_put_contents("Diyorbekahmadjonov/$fromid.channel","false");
file_put_contents("Diyorbekahmadjonov/$fromid.login","false");
      Diyorbekahmadjonov("sendMessage",[
      "chat_id"=>$refid,
"text"=>"<b>👏 Tabriklaymiz! Siz do'stingiz</b> <a href='tg://user?id=$chatid'>foydalanuvchi</a><b>ni botga taklif qildingiz!</b>\n<b>Do'stingiz kanalimizga a'zo bo'lmagunicha, biz sizga referal Puli taqdim etmaymiz!</b>",
"parse_mode"=>"html",
]);
}
}
}
}

if($callbackdata=="result" and ($banid==false)){
addstat($from_id);
if((joinchat($from_id)=="true")  and ($banid==false)){
if(phonenumber($from_id)=="true"){
if($userid==true){
$result = "@$userid";
}else{
$result = "$first_name";
}
Diyorbekahmadjonov("deleteMessage",[
"chat_id"=>$from_id,
"message_id"=>$message_id,
]);
$reply = Diyorbekahmadjonov("sendMessage",[
"chat_id"=>$from_id,
"text"=>"<b>Quyidagi havolani doʻstlaringizga tarqatib Pul ishlang!</b> 👇",
"parse_mode"=>"html",
"reply_markup"=>$menu,
])->result->message_id;
Diyorbekahmadjonov("sendPhoto",[
    "chat_id"=>$from_id,
"photo"=>"https://t.me/TgFOYDALi_BOTLAR/307",
    "caption"=>"✅ <b>@TgShartBor tanlovining rasmiy boti</b> 🤖\n\n🎈 $result do'stingizdan unikal havola-taklifnoma.\n\n👇 Boshlash uchun bosing:\nhttps://t.me/$botname?start=$from_id",
"parse_mode"=>"html",
"reply_to_message_id"=>$reply,
"disable_web_page_preview"=>true,
"reply_markup"=>json_encode([
"inline_keyboard"=>[
[["text"=>"↗️ Doʻstlarga yuborish","switch_inline_query"=>$from_id],],
]
]),
]);
}
$time =  microtime(true);
$random  = rand(999999,3456789);
usleep($random);
$current  = microtime(true)-$time;
usleep($current);
if($referalsum==true){
if(file_exists("Diyorbekahmadjonov/".$from_id.".referalid")){
$referalid = file_get_contents("Diyorbekahmadjonov/".$from_id.".referalid");
if(joinchat($referalid)=="true"){
$is_user = file_get_contents("Diyorbekahmadjonov/".$from_id.".channel");
$login = file_get_contents("Diyorbekahmadjonov/".$from_id.".login");
if($is_user=="false" and $login=="false"){
$minimal = $referalsum / 2;
$user = file_get_contents("Diyorbekahmadjonov/".$referalid.".Pul");
$user = $user + $minimal;
file_put_contents("Diyorbekahmadjonov/".$referalid.".Pul","$user");
$referal = file_get_contents("Diyorbekahmadjonov/".$referalid.".referal");
$referal = $referal + 1;
file_put_contents("Diyorbekahmadjonov/".$referalid.".referal",$referal);
file_put_contents("Diyorbekahmadjonov/".$from_id.".channel","true");
$firstname = str_replace(["<",">","/"],["","",""],$firstname);
Diyorbekahmadjonov("sendMessage",[
"chat_id"=>$referalid,
"text"=>"<b>👏 Tabriklaymiz! Sizning do'stingiz</b> <a href='tg://user?id=".$from_id."'>".$first_name."</a> <b>kanallarga a'zo bo'ldi.</b>\n<b>Sizga ".$minimal." so'm taqdim etildi!</b>\n<b>Do'stingiz roʻyxatdan oʻtsa, sizga yana ".$minimal." so'm taqdim etiladi!</b>",
"parse_mode"=>"html",
"reply_markup"=>$menu,
]);
}
}
}
}
}else{
Diyorbekahmadjonov("answerCallbackQuery",[
"callback_query_id"=>$id,
"text"=>"Siz hali kanallarga aʼzo boʻlmadingiz!",
"show_alert"=>false,
]);
}
}

if($callbackdata=="prodPultion" and $banid==false){
if((joinchat($from_id)=="true") and (phonenumber($from_id)=="true") and ($banid==false)){
if($sumid>=$minimalsumma){
    Diyorbekahmadjonov("deleteMessage",[
    "chat_id"=>$chat_id,
    "message_id"=>$message_id,
]);
 Diyorbekahmadjonov("sendMessage",[
    "chat_id"=>$chat_id,
          "text"=>"💰 <b>Sizning hisobingizda: $sumid so'm mavjud!</b>\n<b>Pulingizni yechib olish uchun hamyonlarni birini tanlang!</b>",
          "parse_mode"=>"html",
          "reply_markup"=>json_encode([
              "inline_keyboard"=>[
                  [["text"=>"💳 Click","callback_data"=>"click"],["text"=>"™️ Paynet","callback_data"=>"paynet"],],
                  [["text"=>"⬅️ Ortga","callback_data"=>"back"],],
                  ]
                  ])
                  ]);
        }else{
          $som = $minimalsumma - $sumcallback;
          Diyorbekahmadjonov("answerCallbackquery",[
              "callback_query_id"=>$id,
              "text"=>"☝️ Sizning hisobingizda mablag' yetarli emas!\nSizga yana mablag'ni yechib olish uchun $som so'm kerak!\nSizning hisobingizda: $sumid so'm mavjud!",
              "show_alert"=>true,
]);
}
}
}

if($callbackdata=="paynet" and $banid==false){ 
if((joinchat($from_id)=="true") and (phonenumber($from_id)=="true") and ($banid==false)){
if($sumid>=$minimalsumma){
  $paynet = file_get_contents("Diyorbekahmadjonov/$chat_id.paynet");
          Diyorbekahmadjonov("deleteMessage",[
    "chat_id"=>$chat_id,
    "message_id"=>$message_id,
]);
 Diyorbekahmadjonov("sendMessage",[
    "chat_id"=>$chat_id,
              "text"=>"❗️ Paynet qilmoqchi bo'lgan telefon raqamingizni kiriting!\nNa'muna: 998901234567",
          "reply_markup"=>json_encode([
             "one_time_keyboard"=>true,
"resize_keyboard"=>true,
    "keyboard"=>[
            [["text"=>"$paynet"],],
    [["text"=>"⬅️ Ortga"],],
                  ]
                  ])
                  ]);
stepbot($chat_id,"raqam");
        }else{
          $som = $minimalsumma - $sumcallback;
          Diyorbekahmadjonov("answerCallbackquery",[
              "callback_query_id"=>$id,
              "text"=>"☝️ Sizning hisobingizda mablag' yetarli emas!\nSizga yana mablag'ni yechib olish Pulhun $som so'm kerak!\nSizning hisobingizda: $sumid so'm mavjud!",
              "show_alert"=>true,
]);
}
}
}

if($step=="raqam" and $ban==false){
if(strlen($text)==12){
if($sum>=$minimalsumma){
if((joinchat($fromid)=="true") and (phonenumber($fromid)=="true") and ($ban==false)){
$hisob = file_get_contents("Diyorbekahmadjonov/$chatid.Pul");
stepbot($chatid,"summa");
              Diyorbekahmadjonov("sendMessage",[
                  "chat_id"=>$chatid,
                  "text"=>"💳 To'lov miqdorini kiriting.\n💰 Sizning hisobingizda: $hisob so'm mavud!",
"reply_markup"=>json_encode([
             "one_time_keyboard"=>true,
"resize_keyboard"=>true,
    "keyboard"=>[
            [["text"=>"$sum"],],
    [["text"=>"⬅️ Ortga"],],
                  ]
                  ])
                  ]);
file_put_contents("Diyorbekahmadjonov/$chatid.paynet","$text");
file_put_contents("Diyorbekahmadjonov/$chatid.raqam","$text");
}
}
    }else{
          Diyorbekahmadjonov("sendMessage",[
              "chat_id"=>$chatid,
              "text"=>"❗️ Paynet qilmoqchi bo'lgan telefon raqamingizni kiriting!\nNa'muna: 998901234567",
              ]);
}
}

if($step=="summa" and $sum>=$minimalsumma and $step!="raqam" and $ban==false){
if($text=="/start" or $text=="⬅️ Ortga"){
unlink("Diyorbekahmadjonovbot/$chatid.step");
}else{
if(stripos($text,"998")!==false){
}else{
$hisob = file_get_contents("Diyorbekahmadjonov/$chatid.Pul");
if($text>=$minimalsumma and $hisob>=$text){
if((joinchat($fromid)=="true") and (phonenumber($fromid)=="true") and ($ban==false)){
$puts = $hisob - $text;
file_put_contents("Diyorbekahmadjonov/$chatid.Pul","$puts");
$jami = file_get_contents("Diyorbekahmadjonov/summa.text");
$jami = $jami + $text;
file_put_contents("Diyorbekahmadjonov/summa.text","$jami");
file_put_contents("Diyorbekahmadjonov/$chatid.textsum","$text");
       $first_name = str_replace(["[","]","|"],["","",""],$firstname);
       Diyorbekahmadjonov("sendMessage",[
           "chat_id"=>$chatid,
           "text"=>"⏰ So'rovlar yakunlandi!\nTo'lov 24 soat ichida amalga oshiriladi!\nTo'lov qilinganligi haqida sizga o'zimiz bot orqali xabar beramiz!",
"reply_markup"=>$menu,
]);
          Diyorbekahmadjonov("sendMessage",[
              "chat_id"=>"-1001299009162",
              "text"=>"💳 Foydalanuvchi Pul yechib olmoqchi!\nKimdan: [$firstname](tg://user?id=$chatid)\nRaqami: $paynet\nTo'lov miqdori: $text so'm",
          "parse_mode"=>"markdown",
          "reply_markup"=>json_encode([
                  "inline_keyboard"=>[
                      [["callback_data"=>"send|$chatid|$firstname","text"=>"💳 To'lov qabul qilindi"]],
[["callback_data"=>"no|$chatid|$firstname","text"=>"💳 To'lov bekor qilindi"]],
[["callback_data"=>"ban|$chatid|$firstname","text"=>"🚫 Ban berish"]],
                        ]
                       ])
                      ]);
unlink("Diyorbekahmadjonovbot/$chatid.step");
        }
}else{
Diyorbekahmadjonov("sendmessage",[
"chat_id"=>$chatid,
            "text"=>"💵 Sizning hisobingizda siz yechib olmoqchi bo'lgan Pul mavjud emas!\nSiz faqat $hisob so'm Pulni yechib olishingiz mumkin!",
          ]);
unlink("Diyorbekahmadjonovbot/$chatid.step");
}
}
}
}

if($callbackdata=="click" and $banid==false){
if($sumid>=$minimalsumma){
if((joinchat($from_id)=="true") and (phonenumber($from_id)=="true") and ($banid==false)){
$clickraqam = file_get_contents("Diyorbekahmadjonov/$chat_id.click");
     Diyorbekahmadjonov("deleteMessage",[
    "chat_id"=>$chat_id,
    "message_id"=>$message_id,
]);
 Diyorbekahmadjonov("sendMessage",[
    "chat_id"=>$chat_id,
              "text"=>"❗️ Click karta raqamingizni kiriting!\nNa'muna: 8600000000000000",
          "reply_markup"=>json_encode([
             "one_time_keyboard"=>true,
"resize_keyboard"=>true,
    "keyboard"=>[
            [["text"=>"$clickraqam"],],
                  [["text"=>"⬅️ Ortga"],],
                  ]
                  ])
                  ]);
stepbot($chat_id,"clickraqam");
        }else{
          $som = $minimalsumma - $sum;
          Diyorbekahmadjonov("answerCallbackquery",[
              "callback_query_id"=>$id,
              "text"=>"☝️ Sizning hisobingizda mablag' yetarli emas!\nSizga yana mablag'ni yechib olish Pulhun $som so'm kerak!\nSizning hisobingizda: $sumid so'm mavjud!",
              "show_alert"=>true,
]);
}
}
}

if($step=="clickraqam" and $ban==false){
if(strlen($text)==16){
if($sum>=$minimalsumma){
if((joinchat($fromid)=="true") and (phonenumber($fromid)=="true") and ($ban==false)){
$hisob = file_get_contents("Diyorbekahmadjonov/$chatid.Pul");
stepbot($chatid,"clicksumma");
              Diyorbekahmadjonov("sendMessage",[
                  "chat_id"=>$chatid,
                  "text"=>"💳 To'lov miqdorini kiriting.\n💰 Sizning hisobingizda: $hisob so'm mavud!",
"reply_markup"=>json_encode([
             "one_time_keyboard"=>true,
"resize_keyboard"=>true,
    "keyboard"=>[
            [["text"=>"$sum"],],
    [["text"=>"⬅️ Ortga"],],
                  ]
                  ])
                  ]);
              file_put_contents("Diyorbekahmadjonov/$chatid.click","$text");
file_put_contents("Diyorbekahmadjonov/$chatid.raqam","$text");
}
}
}else{
Diyorbekahmadjonov("sendMessage",[
"chat_id"=>$chatid,
"text"=>"❗️ Click karta raqamingizni kiriting!\nNa'muna: 8600000000000000",
              ]);
      }
    }

if($step=="clicksumma" and $sum>=$minimalsumma and $step!="clickraqam" and $ban==false){
if($text=="/start" or $text=="⬅️ Ortga"){
Diyorbekahmadjonov("Diyorbekahmadjonovbot/$chatid.step");
}else{
if(stripos($text,"8600")!==false){
}else{
$hisob = file_get_contents("Diyorbekahmadjonov/$chatid.Pul");
if($text>=$minimalsumma and $hisob>=$text){
if((joinchat($fromid)=="true") and (phonenumber($fromid)=="true") and ($ban==false)){
$puts = $hisob - $text;
file_put_contents("Diyorbekahmadjonov/$chatid.Pul","$text");
file_put_contents("Diyorbekahmadjonov/$chatid.Pul","$puts");
$jami = file_get_contents("Diyorbekahmadjonov/summa.text");
$jami = $jami + $text;
file_put_contents("Diyorbekahmadjonov/summa.text","$jami");
file_put_contents("Diyorbekahmadjonov/$chatid.textsum","$text");
       $firstname = str_replace(["[","]","|"],["","",""],$firstname);
       Diyorbekahmadjonov("sendMessage",[
           "chat_id"=>$chatid,
           "text"=>"⏰ So'rovlar yakunlandi!\nTo'lov 24 soat ichida amalga oshiriladi!\nTo'lov qilinganligi haqida sizga o'zimiz bot orqali xabar beramiz!",
"reply_markup"=>$menu,
]);
          Diyorbekahmadjonov("sendMessage",[
              "chat_id"=>"-1001299009162",
              "text"=>"💳 Foydalanuvchi Pul yechib olmoqchi!\nKimdan: [$firstname](tg://user?id=$chatid)\nRaqami: $click\nTo'lov miqdori: $text so'm",
          "parse_mode"=>"markdown",
          "reply_markup"=>json_encode([
                  "inline_keyboard"=>[
                      [["callback_data"=>"send|$chatid|$firstname","text"=>"💳 To'lov qabul qilindi"]],
[["callback_data"=>"no|$chatid|$firstname","text"=>"💳 To'lov bekor qilindi"]],
[["callback_data"=>"ban|$chatid|$firstname","text"=>"🚫 Ban berish"]],
                        ]
                       ])
                      ]);
                      unlink("Diyorbekahmadjonovbot/$chatid.step");
                    }
                    }else{
          Diyorbekahmadjonov("sendMessage",[
              "chat_id"=>$chatid,
            "text"=>"💵 Sizning hisobingizda siz yechib olmoqchi bo'lgan Pul mavjud emas!\nSiz faqat $hisob so'm Pulni yechib olishingiz mumkin!",
              "reply_markup"=>$menu,
]);
unlink("Diyorbekahmadjonovbot/$chatid.step");
}
}
}
}
//@Diyorbek_Ahmadjonov Telegram kanalimizga obuna boling
if((stripos($callbackdata,"send|")!==false) and ($from_id=="238296397")){
    Diyorbekahmadjonov("deleteMessage",[
    "chat_id"=>$chat_id,
    "message_id"=>$message_id,
]); 
       $ex = explode("|",$callbackdata);
       $id = $ex[1];
       $name = $ex[2];
$raqam = file_get_contents("Diyorbekahmadjonov/$id.raqam");
$referal = file_get_contents("Diyorbekahmadjonov/$id.referal");
$miqdor = file_get_contents("Diyorbekahmadjonov/$id.textsum");
Diyorbekahmadjonov("sendMessage",[
"chat_id"=>"-1001458083780",
"text"=>"*💳 Foydalanuvchi Puli toʻlab berildi!*\n\n🗣 *Ismi*: [$name](tg://user?id=$id)\n🔢 *Raqami:* `$raqam`\n*👥 Taklif qilgan aʼzolari:* `$referal`\n💰 *To'lov miqdori:* `$miqdor` *so'm*\n\n✅ *Muvaffaqiyatli oʻtkazildi!*",
"parse_mode"=>"markdown",
]);
       Diyorbekahmadjonov("sendMessage",[
              "chat_id"=>$id,
              "text"=>"<b>Assalom-u alaykum, $name!</b>\n<b>Sizning botdan yechib olgan Pulingiz to'lab berildi!\nIltimos, o'z fikringizni qoldiring!</b>",
              "parse_mode"=>"html",
               "reply_markup"=>json_encode([   
   "inline_keyboard"=>[
[["text"=>"👨‍💻 Admin","url"=>"https://telegram.me/XOJIAKBAR_KAMOLOV_2005"],["text"=>"👥 Kanalimiz","url"=>"https://t.me/TgShartBor"],],
]
]),
]);
}

if((stripos($callbackdata,"no|")!==false) and ($from_id=="238296397")){
        Diyorbekahmadjonov("deleteMessage",[
    "chat_id"=>$chat_id,
    "message_id"=>$message_id,
]); 
       $ex = explode("|",$callbackdata);
       $id = $ex[1];
       $name = $ex[2];
       Diyorbekahmadjonov("sendMessage",[
              "chat_id"=>$id,
              "text"=>"<b>Assalom-u alaykum, $name!</b>\n<b>Sizning botdan yechib olgan Pulingiz bekor qilindi!</b>",
              "parse_mode"=>"html",
               "reply_markup"=>$menu,
]);
}
//@Diyorbek_Ahmadjonov Telegram kanalimizga obuna boling
if((stripos($callbackdata,"ban|")!==false) and ($from_id=="238296397")){
        Diyorbekahmadjonov("deleteMessage",[
    "chat_id"=>$chat_id,
    "message_id"=>$message_id,
]); 
       $ex = explode("|",$callbackdata);
       $id = $ex[1];
       $name = $ex[2];
file_put_contents("Diyorbekahmadjonov/$id.ban","ban");
Diyorbekahmadjonov("sendMessage",[
"chat_id"=>$id,
"text"=>"<b>Hurmatli foydalanuvchi!</b>\n<b>Siz botdan blocklandingiz. Shuning Pulhun botni ishlata olmaysiz!</b>",
"parse_mode"=>"html",
"reply_markup"=>json_encode([
"inline_keyboard"=>[
[["text"=>"📃 Batafsil maʼlumot","callback_data"=>"sabab"],],
]
]),
]);
}
//@Diyorbek_Ahmadjonov Telegram kanalimizga obuna boling
if(mb_stripos($query,"$inlineid")!==false){
$user = $update->inline_query->from->username;
$firstname = $update->inline_query->from->first_name;
if($user){
$username = "@$user";
}else{
$username = "$firstname";
}
Diyorbekahmadjonov("answerInlineQuery",[
"inline_query_id"=>$update->inline_query->id,
"cache_time"=>1,
"results"=>json_encode([[
"type"=>"article",
"id"=>base64_encode(1),
"title"=>"🎈 Unikal havola-taklifnoma",
"description"=>"$username doʻstingizdan unikal havola-taklifnoma",
"thumb_url"=>"http://u1961.xvest4.ru/Omadlikun/INDEX.jpg",
"input_message_content"=>[
"disable_web_page_preview"=>true,
"parse_mode"=>"html",
"message_text"=>"✅ <b>@TgShartBor tanlovining rasmiy boti</b> 🤖\n\n🎈 $username do'stingizdan unikal havola-taklifnoma.\n\n👇 Boshlash uchun bosing:
https://t.me/$botname?start=$inlineid"],
"reply_markup"=>[
"inline_keyboard"=>[
[["text"=>"🚀 Boshlash","url"=> "https://t.me/$botname?start=$inlineid"],],
]]
],
])
]);
}
//@Diyorbek_Ahmadjonov Telegram kanalimizga obuna boling
if($text=="🗒 Qo‘llanma" and $ban==false){
if((joinchat($fromid)=="true") and (phonenumber($fromid)=="true") and ($ban==false)){
Diyorbekahmadjonov('sendMessage',[
"chat_id"=>$chatid,
"text"=>"<b>
@TgShartBor sayti navbatdagi yutuqli aksiyani o‘tkazmoqda. Barchasi haqqoniy va halol bo‘lishiga kafolat beramiz.
 
Qo‘llanma
 
⁉️ 1-savol: Bu aksiya orqali qanday qilib pul ishlashim mumkin?
 
✅ Javob: Siz tanlovga taklif qilgan va barcha shartlarni bajargan har bir do‘stingiz uchun sizga 1000 so‘m mukofot puli beriladi.
Masalan:
— 10 nafar do‘stingiz uchun 10 000 so‘m
— 100 nafar do‘stingiz uchun 100 000 so‘m va hokazo.
 
⁉️ 2-savol: Ishlab topilgan pul qanday chiqarib olinadi?
 
✅ Javob: Ishlab topgan pulingiz 50 ming so‘mga yetganda, uni telefon raqamingiz yoki karta hisob raqamingizga o‘tkazib olishingiz mumkin. Mablag‘lar Click tizimi orqali Uzcard va Humo kartalariga yoki Ucell, Beeline, Uzmobile, Mobiuz (UMS) va Perfectum abonentlarining hisob raqamiga o‘tkaziladi.
 

⁉️ 3-savol: Qanday holatlarda jarima qo‘llanadi?
 
✅ Javob: Siz taklif etgan do‘stingiz barcha kanallarga a‘zo bo‘lgach, sizga 1000so‘m to‘lanadi. Agar do‘stingiz kanallardan biri yoki bir nechtasidan chiqib ketsa, u holda uning uchun sizga to‘langan 1000 so‘m avtomatik qaytarib olinadi.</b>",
"parse_mode"=>"html",
"reply_markup"=>$menu,
]);
}
}

if($text=="📊 Hisobot" and $ban==false){
if((joinchat($fromid)=="true") and (phonenumber($fromid)=="true") and ($ban==false)){
$userlar = file_get_contents("Diyorbekahmadjonov.bot");
$count = substr_count($userlar,"\n");
$member = count(file("Diyorbekahmadjonov.bot"))-1;
$banusers = file_get_contents("Diyorbekahmadjonov.ban");
$bancount = substr_count($userlar,"\n");
$banmember = count(file("Diyorbekahmadjonov.ban"))-1;
    Diyorbekahmadjonov("sendMessage",[
"chat_id"=>$chatid,
"text"=>"<b>Botimiz a'zolari soni:</b> <code>$member</code>\n<b>Qora roʻyxatdagi a'zolar soni:</b> <code>$banmember</code>\n<b>Siz botga taklif qilgan aʼzolar soni:</b> <code>$referal</code>\n\n$sana-$soat",
"parse_mode"=>"html",
"reply_markup"=>json_encode([
"inline_keyboard"=>[
[["text"=>"♻️ Yangilash","callback_data"=>"upgrade"],],
]
]),
]);
}
}

if($callbackdata=="upgrade" and $banid==false){
if((joinchat($from_id)=="true") and (phonenumber($from_id)=="true") and ($banid==false)){
$referal = file_get_contents("Diyorbekahmadjonov/$chat_id.referal");
$userlar = file_get_contents("Diyorbekahmadjonov.bot");
$count = substr_count($userlar,"\n");
$member = count(file("Diyorbekahmadjonov.bot"))-1;
$banusers = file_get_contents("Diyorbekahmadjonov.ban");
$bancount = substr_count($userlar,"\n");
$banmember = count(file("Diyorbekahmadjonov.ban"))-1;
Diyorbekahmadjonov("editMessageText",[
"chat_id"=>$chat_id,
"message_id"=>$message_id,
"text"=>"<b>Botimiz a'zolari soni:</b> <code>$member</code>\n<b>Qora roʻyxatdagi a'zolar soni:</b> <code>$banmember</code>\n<b>Siz botga taklif qilgan aʼzolar soni:</b> <code>$referal</code>\n\n$sana-$soat",
"parse_mode"=>"html",
"reply_markup"=>json_encode([
"inline_keyboard"=>[
[["text"=>"♻️ Yangilash","callback_data"=>"upgrade"],],
]
]),
]);
Diyorbekahmadjonov("answerCallbackQuery",[
"callback_query_id"=>$id,
"text"=>"Botimiz a'zolari soni: $member\nQora roʻyxatdagi a'zolar soni: $banmember\nSiz botga taklif qilgan aʼzolar soni: $referal\n\n$sana-$soat",
"show_alert"=>true,
]);
}
}

if($text=="💌 Biz bilan aloqa" and $ban==false){
if((joinchat($fromid)=="true") and (phonenumber($fromid)=="true") and ($ban==false)){
Diyorbekahmadjonov("sendMessage",[
   "chat_id"=>$chatid,
   "text"=>"Bizga aloqaga chiqishdan oldin tanlov qo'llanmasi bilan tanishib chiqing
 
📞 Aloqa markazi: @XOJIAKBAR_KAMOLOV",
"parse_mode"=>"html",
"reply_markup"=>json_encode([
"inline_keyboard"=>[
[["text"=>"🗣 Bog'lanish","url"=>"https://t.me/XOJIAKBAR_KAMOLOV_2005"],],
]
]),
]);
}
}

if($text=="👨‍💻 Dasturchi" and $ban==false){
if((joinchat($fromid)=="true") and (phonenumber($fromid)=="true") and ($ban==false)){
Diyorbekahmadjonov("sendPhoto",[
"chat_id"=>$chatid,
"photo"=>"https://t.me/TgFOYDALi_BOTLAR/308",
"caption"=>"<b>Bot dasturchisi:</b> <a href='tg://user?id=1245678232'>XOJIAKBAR_KAMOLOV</a>\n\n<b>Ish vaqti: 08:00 dan 23:00 gacha</b>\n\n<b>Diqqat! Bot Pul to'lab berish yoki to'lab bermasligiga dasturchi javobgar emas!</b>",
"parse_mode"=>"html",
"reply_markup"=>json_encode([
"inline_keyboard"=>[
[["text"=>"♻️ Bogʻlanish","url"=>"https://t.me/XOJIAKBAR_KAMOLOV_2005"],],
]
]),
]);
}
}

if($ban==true){
Diyorbekahmadjonov("deleteMessage",[
"chat_id"=>$chatid,
"message_id"=>$messageid,
]);
Diyorbekahmadjonov("sendMessage",[
"chat_id"=>$chatid,
"text"=>"<b>Hurmatli foydalanuvchi!</b>\n<b>Siz botdan banlangansiz. Shuning Pulhun botni ishlata olmaysiz!</b>",
"parse_mode"=>"html",
"reply_markup"=>json_encode([
"inline_keyboard"=>[
[["text"=>"📃 Batafsil maʼlumot","callback_data"=>"sabab"],],
]
]),
]);
}

if($banid==true){
Diyorbekahmadjonov("deleteMessage",[
"chat_id"=>$chat_id,
"message_id"=>$message_id,
]);
Diyorbekahmadjonov("sendMessage",[
"chat_id"=>$chat_id,
"text"=>"<b>Hurmatli foydalanuvchi!</b>\n<b>Siz botdan banlangansiz. Shuning Pulhun botni ishlata olmaysiz!</b>",
"parse_mode"=>"html",
"reply_markup"=>json_encode([
"inline_keyboard"=>[
[["text"=>"📃 Batafsil maʼlumot","callback_data"=>"sabab"],],
]
]),
]);
}

if($callbackdata=="sabab"){
Diyorbekahmadjonov("answerCallbackQuery",[
"callback_query_id"=>$id,
"text"=>$sabab,
"show_alert"=>true,
]);
}
