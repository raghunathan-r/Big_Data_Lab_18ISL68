# Big Data Lab

## Exercise 2 Hadoop

-[] Properly read and understand the version that you are installing

## Exercise 5 Hive

How to install Hive in Ubuntu 20 [https://phoenixnap.com/kb/install-hive-on-ubuntu]

import java.util.*;

import javax.management.loading.PrivateClassLoader;

import java.io.IOException;
import org.apache.hadoop.fs.Path;
import org.apache.hadoop.http.lib.StaticUserWebFilter.StaticUserFilter;
import org.apache.hadoop.conf.*;
import org.apache.hadoop.mapred.*;
import org.apache.hadoop.util.*;
import org.apache.hadoop.io.*;
public class WordCou {

public static class Map extends MapReduceBase implements Mapper<LongWritable,Text,Text,IntWritable>
{
private static IntWritable one=new IntWritable(1);
private Text word=new Text();
@Override
public void map(LongWritable key, Text value, OutputCollector<Text, IntWritable> output, Reporter reporter)
throws IOException {
// TODO Auto-generated method stube

String line=value.toString();
StringTokenizer toc=new StringTokenizer(line);
while(toc.hasMoreTokens())
{
word.set(toc.nextToken());
output.collect(word, one);
}


}

}
public static class Reduce extends MapReduceBase implements Reducer<Text, IntWritable, Text, IntWritable>
{

@Override
public void reduce(Text key, Iterator<IntWritable> values, OutputCollector<Text, IntWritable> output, Reporter reporter)
throws IOException {
// TODO Auto-generated method stub
int sum=0;
while(values.hasNext())
{
sum+=values.next().get();
}
output.collect(key, new IntWritable(sum));
}

}
public static void main(String []args) throws Exception
{
JobConf conf=new JobConf(WordCou.class);
conf.setJobName("word count");
conf.setOutputKeyClass(Text.class);
conf.setOutputValueClass(IntWritable.class);
conf.setMapperClass(Map.class);
conf.setCombinerClass(Reduce.class);
    conf.setReducerClass(Reduce.class);
    conf.setInputFormat(TextInputFormat.class);
    conf.setOutputFormat(TextOutputFormat.class);
    FileInputFormat.setInputPaths(conf, new Path(args[0]));
    FileOutputFormat.setOutputPath(conf, new Path(args[1]));
    JobClient.runJob(conf);

}
}
