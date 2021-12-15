# Laba11_Evgenia
1)Создаём проект

2)Помещяаем на форму 2 компонента типа TextEdit – один для ввода телефонного номера, 
другой для ввода текста СМС-сообщения

3)Помещяаем на форму 2 компонента типа Button – один для кнопки «Звонок»,
другой для кнопки «СМС».
![image](https://user-images.githubusercontent.com/73265788/146134519-f3f4a3f9-366a-4ff7-8c53-ee406a6ec9f7.png)


Добавим разрешения на осуществления вызова
и отправки СМС в файле AndroidManifest.xml

![image](https://user-images.githubusercontent.com/73265788/146134558-c887d62d-17f0-46df-884c-4a34199e8cd3.png)

Добавляем обработчик события по кнопке «Отправить сообщение»:
```Java
       public void onSms(View view) {
            EditText edit_Number=(EditText)findViewById(R.id.editTextPhone);
            String phoneNo = edit_Number.getText().toString();
            EditText sms_edit=(EditText)findViewById(R.id.editTextTextMultiLine2);
            String toSms="smsto:"+edit_Number.getText().toString();
            String messageText= sms_edit.getText().toString();
            Intent sms=new Intent(Intent.ACTION_SENDTO, Uri.parse(toSms));
            sms.putExtra("sms_body", messageText);
            startActivity(sms);
            SmsManager.getDefault().sendTextMessage(phoneNo, null,
                    messageText.toString(), null, null);
        }         
```
Внесим изменения в функцию «onCreate»:
```Java
protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        Button mDialButton = (Button) findViewById(R.id.button2);
        final EditText mPhoneNoEt = (EditText)
                findViewById(R.id.editTextPhone);
        final EditText smsEdit = (EditText) findViewById(R.id.editTextTextMultiLine2);
        mDialButton.setOnClickListener(new View.OnClickListener()
        {
            @Override
            public void onClick(View view)
            {
                String phoneNo = mPhoneNoEt.getText().toString();
                if(!TextUtils.isEmpty(phoneNo))
                {
                    String dial = "tel:" + phoneNo;
                    startActivity(new Intent(Intent.ACTION_CALL,
                            Uri.parse(dial)));
                }
                else {
                    Toast.makeText(MainActivity.this, "Введите номер телефона",
                            Toast.LENGTH_SHORT).show();
                }
            }
        });
    }
```
    
    
    
 Запускаем и проверяем приложение:
 
 
 
 ![image](https://user-images.githubusercontent.com/73265788/146135219-cff4fa56-ea7b-45ea-9aad-6eb33ce3b8c7.png)

![image](https://user-images.githubusercontent.com/73265788/146135272-6a71078a-283c-44fa-a688-5b8bde0d3027.png)

    
