HADOOP KURULUMU / INSTALLATION

Öncelikle mevcut Centos7 işletim sistemimimiz güncelleştirilir. Aşağıda komutlar mevcuttur. 

sudo yum install epel-release -y
sudo yum update -y

OR

yum install epel-release -y
yum update -y

JAVA YÜKLEME ADIMLARI

sudo yum install -y java-1.8.0-openjdk

OR 

yum install -y java-1.8.0-openjdk
yüklendiğini alttaki komut satırı ile birlikte teyit edebiliriz.

java -version

Çıktı aşağıda olduğu gibi olmalıdır.

openjdk version "1.8.0_111"
OpenJDK Runtime Environment (build 1.8.0_111-b15)
OpenJDK 64-Bit Server VM (build 25.111-b15, mixed mode)

HADOOP YÜKLEME ADIMLARI

wget http://www-us.apache.org/dist/hadoop/common/hadoop-2.7.3/hadoop-2.7.3.tar.gz burada örnek olarak hadoop URLsi verilmiştir mevcut
ve yeni sürümleri yükleyebilmek için https://hadoop.apache.org/releases.html bu siteye erişmemiz gerekiyor.

Site içerisinde en güncel olanını sanal makinelere yükleyeceğimiz için BinaryDownload sütunundan seçilmesi gereklidir. 
http://ftp.itu.edu.tr/Mirror/Apache/hadoop/common/hadoop-3.1.3/hadoop-3.1.3.tar.gz bunu alarak aşağıdaki şekilde dosyayı yüklüyoruz.

wget http://ftp.itu.edu.tr/Mirror/Apache/hadoop/common/hadoop-3.1.3/hadoop-3.1.3.tar.gz

Aşağıda yazılan komutlarla birlikte indirilen tar dosyası dizine çıkarılır ve /opt dosyasına kopyalanır. cd komutu ile /opt dizinine
erişilir ve mv komutu ile mevcut çıkartılmış olan dosya yeni hadoop ismiyle birlikte değiştirilir.
tar -xzf hadoop-3.1.3.tar.gz -C /opt
cd /opt
mv hadoop-3.2.1 hadoop

