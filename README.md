<?php
use Qcloud\Sms\SmsSingleSender;

class Sms extends CI_Controller {
    public function index()
    {
        $data = $this->input->get();
        // 需要发送短信的手机号码  $data['phone']
        // var_dump($data['phone']);die;
        // 短信应用 SDK AppID
        $appid = 1400567890; // SDK AppID 以1400开头
        // 短信应用 SDK AppKey
        $appkey = "25ksjfkdsjfkdsjfk***************";
        // 短信模板 ID，需要在短信控制台中申请
        $templateId = 7839;  // NOTE: 这里的模板 ID`7839`只是示例，真实的模板 ID 需要在短信控制台中申请
        $smsSign = "腾讯云"; // NOTE: 签名参数使用的是`签名内容`，而不是`签名ID`。这里的签名"腾讯云"只是示例，真实的签名需要在短信控制台申请
        $val_1 = str_pad(random_int(1, 9999), 4, 0, STR_PAD_LEFT); // 短信内容形参 1
        $val_2 = 3;  // 短信内容形参 2

        try {
          $ssender = new SmsSingleSender($appid, $appkey);
          $result = $ssender->send(0, "86", $data['phone'],
              "{$val_1}为您的登录验证码，请于{$val_2}分钟内填写。如非本人操作，请忽略本短信。", "", "");
          // "{$val_1}为您的登录验证码，请于{$val_2}分钟内填写。如非本人操作，请忽略本短信。" 这个是你申请短信模板里短信正文的内容
          $rsp = json_decode($result);
          var_dump($rsp);die;  // 这个是测试的时候打印一下信息
          echo $result;
        } catch(\Exception $e) {
          echo var_dump($e);
        }

    }
}

