# nano /etc/hostname
mail.tkj.com
# nano /etc/hosts
127.0.1.1 mail.tkj.com
#reboot
#apt update
#apt install postfix mailutils
#dpkg-reconfigure postfix

#nano /etc/postfix/main.cf
relayhost = [smtp.gmail.com]:587
smtp_sasl_auth_enable = yes
smtp_sasl_security_options = noanonymous
smtp_sasl_password_maps = hash:/etc/postfix/sasl/sasl_passwd
smtp_tls_security_level = encrypt
smtp_tls_CAfile = /etc/ssl/certs/ca-certificates.crt
myhostname = mail.tkj.com

#nano /etc/postfix/sasl/sasl_passwd
[smtp.gmail.com]:587 namaemail@gmail.com:passwordemail

#postmap /etc/postfix/sasl/sasl_passwd
# rm /etc/postfix/sasl/sasl_passwd
#chown root:root /etc/postfix/sasl/sasl_passwd.db
#chmod 600 /etc/postfix/sasl/sasl_passwd.db
#/etc/init.d/postfix restart
#aktifkan less secure app pada akun google
https://myaccount.google.com/lesssecureapps

#aktifkan IMAP pada Gmail
#test kirim email
echo "haii" | mail -s "test SMTP Relay" namaemail@gmail.com

#merubah nama user email
getent passwd $USER
chfn -f "FirstName LastName" root