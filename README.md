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

Setup environmental variables(Çevresel değişkenleri ayarlama)

"vi .bashrc" komutu ile en alt satıra aşağıda bulunan komutlar yazılır.

export JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.212.b04-0.el7_6.x86_64/jre   ## Change it according to your system
export HADOOP_HOME=/home/hadoop/hadoop   ## Change it according to your system
export HADOOP_INSTALL=$HADOOP_HOME
export HADOOP_MAPRED_HOME=$HADOOP_HOME
export HADOOP_COMMON_HOME=$HADOOP_HOME
export HADOOP_HDFS_HOME=$HADOOP_HOME
export HADOOP_YARN_HOME=$HADOOP_HOME
export HADOOP_COMMON_LIB_NATIVE_DIR=$HADOOP_HOME/lib/native
export PATH=$PATH:$HADOOP_HOME/sbin:$HADOOP_HOME/bin

ardından "source .bashrc" komutu ile birlikte yapılan işlemler kayıt edilir.

Modify Configuration files(Yapılandırma Dosyalarını Değiştir)

vi $HADOOP_HOME/etc/hadoop/hadoop-env.sh komutu ile açılan ekran içerisine mevcut bulunan export JAVA_HOME dosyası aşağıda yazdığı gibi değiştirilir.

export JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.212.b04-0.el7_6.x86_64/jre

Hadoop içerisinde birçok configuration dosyası bulunmaktadır.

cd $HADOOP_HOME/etc/hadoop iler configuration dosyalarının bulunduğu dizine gidilir.

core-site.xml dosyası içerisine girilir. Configuration taglerinin arasına aşağıda bulunan şekilde yerleştirilir.


<configuration>
        <property>
                <name>fs.defaultFS</name>
                <value>hdfs://server.itzgeek.local:9000</value>
        </property>
</configuration>

Diğer dosyanın işlemi bitirildikten sonra hdfs-site.xml içerisine girilir. 

<configuration>
        <property>
                <name>dfs.replication</name>
                <value>1</value>
        </property>
        <property>
                <name>dfs.name.dir</name>
                <value>file:///home/hadoop/hadoopdata/hdfs/namenode</value>
        </property>
        <property>
                <name>dfs.data.dir</name>
                <value>file:///home/hadoop/hadoopdata/hdfs/datanode</value>
        </property>
</configuration>

kodları yazılarak işlemler bitirilir.

Hadoop klasörü içerisine namenode ve datanode adı altında iki klasör oluşturmak için aşağıdaki komut satırı yazılır.

mkdir -p ~/hadoopdata/hdfs/{namenode,datanode}

Bu işlem bittikten sonra mapred-site.xml içerisine girilir.

<configuration>
        <property>
                <name>mapreduce.framework.name</name>
                <value>yarn</value>
        </property>
</configuration> 

bu şekilde ayarlanarak kayıt edilir ve kapatılır.

yarn-site.xml içerisine girilir.

<configuration>
        <property>
                <name>yarn.nodemanager.aux-services</name>
                <value>mapreduce_shuffle</value>
        </property>
</configuration>

kayıt edilir ve kapatılır.

hdfs namenode -format komutu ile birlikte namenode formatlanır.

start-dfs.sh ve start-yarn.sh komutları ile birlikte NameNode, DataNode, ResourceManager ve NodeManager açılır.

