<?php

// У����֤��	@return boolean
   function checkVerify(){
	$verify = new \Think\Verify();
	return $verify->check(I('verify'));
   }

	/**
      * ���Ȩ��
      * @param name string|array  ��Ҫ��֤�Ĺ����б�,֧�ֶ��ŷָ���Ȩ�޹������������
      * @param uid  int           ��֤�û���id
      * @param string mode        ִ��check��ģʽ
      * @param relation string    ���Ϊ 'or' ��ʾ������һ������ͨ����֤;���Ϊ 'and'���ʾ���������й������ͨ����֤
      * @return boolean           ͨ����֤����true;ʧ�ܷ���false
     */
	function authcheck($name, $uid, $type=1, $mode='url', $relation='or'){
		return true;
		//
		if(!in_array($uid,C('ADMINISTRATOR'))){ 
	    	$auth=new \Think\Auth();
	    	return $auth->check($name, $uid, $type, $mode, $relation)?true:false;
	    }else{
	    	return true;
	    }
	}
   
   function display($name){
   	$name='Home/'.$name;
	$uid=session('uid');
	if(!in_array($uid,C('ADMINISTRATOR'))){
	if(!authcheck($name, $uid, $type=1, $mode='url', $relation='or')){
	return "style='display:none'";
	 }
	}
   }
	


function cateTree($pid=0,$level=0,$db=0){
    $cate=M(''.$db.'');
    $array=array();
    $tmp=$cate->where(array('pid'=>$pid))->order("sort")->select();
    if(is_array($tmp)){
        foreach($tmp as $v){
            $v['level']=$level;
            //$v['pid']>0;
            $array[count($array)]=$v;
            $sub=cateTree($v['id'],$level+1,$db);
            if(is_array($sub))$array=array_merge($array,$sub);
        }
    }
    return $array;
}

function orgcateTree($pid=0,$level=0,$type=0){
	/*
    $cate=M('auth_group');
    $array=array();
    $tmp=$cate->where(array('pid'=>$pid,'type'=>$type))->order("sort")->select();
    if(is_array($tmp)){
        foreach($tmp as $v){
            $v['level']=$level;
            //$v['pid']>0;
            $array[count($array)]=$v;
            $sub=orgcateTree($v['id'],$level+1,$type);
            if(is_array($sub))$array=array_merge($array,$sub);
        }
    }
    return $array;
    */
}

function cateTreed($pid=0,$level=0){
    $cate=M('datalist');
    $array=array();
    $tmp=$cate->where(array('pid'=>$pid))->order("sort")->select();
    if(is_array($tmp)){
        foreach($tmp as $v){
		    $v['level']=$level;
            //$v['pid']>0;
            $array[count($array)]=$v;
            $sub=cateTreed($v['id'],$level+1);
            if(is_array($sub))$array=array_merge($array,$sub);
        }
    }
    return $array;
}

/**
 * ��ʽ���ֽڴ�С
 * @param  number $size      �ֽ���
 * @param  string $delimiter ���ֺ͵�λ�ָ���
 * @return string            ��ʽ����Ĵ�λ�Ĵ�С
 * @author ����� <zuojiazi@vip.qq.com>
 */
function format_bytes($size, $delimiter = '') {
    $units = array('B', 'KB', 'MB', 'GB', 'TB', 'PB');
    for ($i = 0; $size >= 1024 && $i < 5; $i++) $size /= 1024;
    return round($size, 2) . $delimiter . $units[$i];
}

/**
 * ����ϵͳ��API�ӿڷ�������̬������
 * api('User/getName','id=5'); ���ù���ģ���User�ӿڵ�getName����
 * api('Admin/User/getName','id=5');  ����Adminģ���User�ӿ�
 * @param  string  $name ��ʽ [ģ����]/�ӿ���/������
 * @param  array|string  $vars ����
 */
function api($name,$vars=array()){
    $array     = explode('/',$name);
    $method    = array_pop($array);
    $classname = array_pop($array);
    $module    = $array? array_pop($array) : 'Common';
    $callback  = $module.'\\Api\\'.$classname.'Api::'.$method;
    if(is_string($vars)) {
        parse_str($vars,$vars);
    }
    return call_user_func_array($callback,$vars);
}

function check_table_exist($tableName){
    $tableName = C('DB_PREFIX') . strtolower($tableName);
    $tables = M()->query('show tables');
    if(empty($tables)){
        exit('��ݿ���û�б�');
    }
    foreach($tables as $v){
        if($v['tables_in_test']==$tableName){
            return true ;
        }
    }
    exit('��ݿ���û�� '.$tableName.' �?�봴��');
}

/**
 * ��������ֶλ�ȡָ��������
 * @param mixed $value ���������ó�����������
 * @param string $condition �����ֶ�
 * @param string $field ��Ҫ���ص��ֶΣ������򷵻�������
 * @param string $table ��Ҫ��ѯ�ı�
 * @author huajie <banhuajie@163.com>
 */
function get_table_field($value = null, $condition = 'id', $field = null, $table = null){
    if(empty($value) || empty($table)){
        return false;
    }

    //ƴ�Ӳ���
    $map[$condition] = $value;
    $info = M(ucfirst($table))->where($map);
    if(empty($field)){
        $info = $info->field(true)->find();
    }else{
        $info = $info->getField($field);
    }
    return $info;
}


function Hex($indata){
	$lX8 = $indata & 0x80000000;
	if($lX8)
	{
		$indata=$indata & 0x7fffffff;
	}
	while ($indata>16)
	{
		$temp_1=$indata % 16;
		$indata=$indata /16 ;
		if($temp_1<10)
		   $temp_1=$temp_1+0x30;
		else
		   $temp_1=$temp_1+0x41-10; 
		
		$outstring= chr($temp_1) . $outstring ; 
		   
	}
	$temp_1=$indata;
	if($lX8)$temp_1=$temp_1+8;
	if($temp_1<10)
	   $temp_1=$temp_1+0x30;
	else
	   $temp_1=$temp_1+0x41-10; 
	
	$outstring= chr($temp_1) . $outstring ; 
	
	return $outstring;
		 
}

/**
 * �ַ�ת��Ϊ���飬��Ҫ���ڰѷָ������ڶ�������
 * @param  string $str  Ҫ�ָ���ַ�
 * @param  string $glue �ָ��
 * @return array
 * @author ����� <zuojiazi@vip.qq.com>
 */
function str2arr($str, $glue = ','){
    return explode($glue, $str);
}

/**
 * ����ת��Ϊ�ַ���Ҫ���ڰѷָ������ڶ�������
 * @param  array  $arr  Ҫ���ӵ�����
 * @param  string $glue �ָ��
 * @return string
 * @author ����� <zuojiazi@vip.qq.com>
 */
function arr2str($arr, $glue = ','){
    return implode($glue, $arr);
}

/**
 * �ַ��ȡ��֧�����ĺ��������
 * @static
 * @access public
 * @param string $str ��Ҫת�����ַ�
 * @param string $start ��ʼλ��
 * @param string $length ��ȡ����
 * @param string $charset �����ʽ
 * @param string $suffix �ض���ʾ�ַ�
 * @return string
 */
function msubstr($str, $start=0, $length) {
	$charset="utf-8";
	$suffix=true;
    if(function_exists("mb_substr"))
        $slice = mb_substr($str, $start, $length, $charset);
    elseif(function_exists('iconv_substr')) {
        $slice = iconv_substr($str,$start,$length,$charset);
        if(false === $slice) {
            $slice = '';
        }
    }else{
        $re['utf-8']   = "/[\x01-\x7f]|[\xc2-\xdf][\x80-\xbf]|[\xe0-\xef][\x80-\xbf]{2}|[\xf0-\xff][\x80-\xbf]{3}/";
        $re['gb2312'] = "/[\x01-\x7f]|[\xb0-\xf7][\xa0-\xfe]/";
        $re['gbk']    = "/[\x01-\x7f]|[\x81-\xfe][\x40-\xfe]/";
        $re['big5']   = "/[\x01-\x7f]|[\x81-\xfe]([\x40-\x7e]|\xa1-\xfe])/";
        preg_match_all($re[$charset], $str, $match);
        $slice = join("",array_slice($match[0], $start, $length));
    }
    return $suffix ? $slice.'' : $slice;
}



function getuserid(){
	return session("uid");
}


function gettruename(){
	return session("truename");
}

function gettime(){
	return date('Y-m-d H:i:s',time());
}

    function encrypt($data) {
        //return md5(C('AUTH_MASK') . md5($data));
		return md5(md5($data));
    }

//html�������
function html_out($str){
    if(function_exists('htmlspecialchars_decode')){
        $str=htmlspecialchars_decode($str);
    }else{
        $str=html_entity_decode($str);
    }
    $str = stripslashes($str);
    return $str;
}

function truename($id){
 $data=M('user')->where('id='.$id)->getField('truename');
 return $data;
}


function comname($id){
 $data=M('cust')->where('id='.$id)->getField('title');
 return $data;
}




