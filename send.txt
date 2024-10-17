<?php
if ($_SERVER["REQUEST_METHOD"] == "POST") {
    // フォームデータを取得
    $name = htmlspecialchars($_POST['name'], ENT_QUOTES, 'UTF-8');
    $date = htmlspecialchars($_POST['date'], ENT_QUOTES, 'UTF-8'); // 日付を取得
    $time1 = htmlspecialchars($_POST['time1'], ENT_QUOTES, 'UTF-8');
    $time2 = htmlspecialchars($_POST['time2'], ENT_QUOTES, 'UTF-8');
    $email = htmlspecialchars($_POST['email'], ENT_QUOTES, 'UTF-8');
    $postcode = htmlspecialchars($_POST['postcode'], ENT_QUOTES, 'UTF-8');
    $address = htmlspecialchars($_POST['address'], ENT_QUOTES, 'UTF-8');
    $phone = htmlspecialchars($_POST['phone'], ENT_QUOTES, 'UTF-8');

    // メールの準備
    $to = "horimoto@dia-niigata.co.jp";
    $subject = "新しいご予約のリクエスト";

    // メール内容
    $message = "
    新しいご予約が送信されました：

    お名前: $name
    ご来場の日付: $date
    第一希望のご来場時間: $time1
    第二希望のご来場時間: $time2
    メールアドレス: $email
    郵便番号: $postcode
    住所: $address
    電話番号: $phone
    ";

    // メールヘッダー
    $headers = "From: $email\r\n";
    $headers .= "Reply-To: $email\r\n";
    $headers .= "Content-Type: text/plain; charset=UTF-8\r\n";

    // メールを送信
    if (mail($to, $subject, $message, $headers)) {
        echo "ご予約が送信されました。";
    } else {
        echo "メールの送信中にエラーが発生しました。";
    }
} else {
    echo "不正なリクエストです。";
}
?>
