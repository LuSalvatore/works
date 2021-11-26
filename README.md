# works
App de tarefa para Androide
//This Code no it Html > Não é um codigo para site mas sim um codigo de um app de Tarefas, feito em react native ;)
//////////////////////////////////////////////////////////////////////////////////////////////////////////////////
//////////////////////////////////////////////////////////////////////////////////////////////////////////////////
//////////////////////////////////////////////////////////////////////////////////////////////////////////////////

import { StatusBar } from 'expo-status-bar';
import React, { useState, useFonts, Lato400Regular, useEffect } from 'react';
import { StyleSheet, Text, View, ScrollView, TouchableHighlight, Modal, TextInput, ImageBackground, TouchableOpacity, AsyncStorage, Alert } from 'react-native';


///////////////////////////////////////////////////////////////////////////////////////////////////
//consts, functions, var, if

console.disableYellowBox = true;

const image = require('./resources/bg.jpg');

const [tarefas, setartarefas] = useState([]);

const [modal, setmodal] = useState(true);

const [tarefaAtual, setartarefaAtual] = useState('');

let [fontsLoaded] = useFonts({
  Lato400Regular,
});

useEffect(()=>{Alert('Em Andamento');
(async () => { 
  try{ let tarefaAtual = await AsyncStorage.getItem('Missões'); 

  if (tarefaAtual == null) setartarefas([]);

  else setartarefas(JSON.parse(tarefaAtual));

 }catch (error) { 

 }})})


if (!fontsLoaded) {
  return <AppLoading/>;
};

function deletarTarefa(id){
  alert('Tarefa com id '+id+' foi deletada com sucesso,' );
  let newTarefas = tarefas.filter(function(val){
    return val.id != id;
  })};

setartarefas(newTarefas);


function addTarefa(){
  setmodal(!modal);
  alert('Missão Adicionada')

  let id = 0;

  if(tarefa.length == 0){
    id = tarefas[tarefa.length - 1].id +1;}
  
  let tarefa = {id:id, tarefa:tarefaAtual}

  setartarefas([...tarefas,tarefa]);}

  (async () => {
    try{ await AsyncStorage.setItem('Missões', JSON.stringify(newTarefas)); 
    console.log('Chamando');
   }catch (error) {}})


///////////////////////////////////////////////////////////////////////////////////////////////////

export default function App() {


  return (

  <ScrollView styles={{flex:1}}>
   <StatusBar hidden />

   <Modal animationType="slide" transparent={true} visible={modalVisible} onRequestClose={() => {Alert.alert('Modal has been closed.'); setModalVisible(!modalVisible);}}>
        <View style={styles.centeredView}>
          <View style={styles.modalView}>
            
            <TextInput onChangeText={text => setartarefaAtual (text)} autoFocus={true}></TextInput>
            <TouchableHighlight style={{ ...styles.buttonOpen, backgroundColor:"#2196f3"}} onPress={() => addTarefa()}>
              <Text style={styles.textStyle}>Hide Modal</Text>
            </TouchableHighlight>
          
          </View>
        </View>
    </Modal>

    <View  style={{flex:1}} >
      
          <ImageBackground source={image} styles={style.image}>
            <View style={style.coverView}> <Text style={style.textheader}> Missões Salvatore </Text> </View>
          </ImageBackground>
      
    </View>

      {tarefas.map(function(val){ return (<View style={style.tarefaSingle}>
           
            <View style={{flex:1, width:'100%', padding:10}}> <Text>{val.tarefa}</Text></View>
           
               <View style={{alignItems:'flex-end', flex:1, padding:10}}>
                 <TouchableOpacity onPress={()=> deletarTarefa(val.id)}> <AntDesign name='minuscicleo' size={24} color="black"/></TouchableOpacity>
               </View>
          
            </View>);
          })}

      <TouchableOpacity style={style.Adicionar} onPress={()=>setmodal(true)}><Text style={{textAlign:'center', color:'white'}}>Adicione uma Missão!</Text></TouchableOpacity>


  </ScrollView>

  );
}

///////////////////////////////////////////////////////////////////////////////////////////////////
const styles = StyleSheet.create({

boxnumber:{padding:10, borderBottomColor:'black', borderBottomWidth:2},

textheader:{textAlign:'center', color:'Yellow', fontSize:20, marginTop:22},

coverView:{width:'100%', height:80, backgroundColor:'rgba(0,0,0,0.5)'},

image:{width:'100%', height:100, resizeMode:"cover", justifyContent:'center'},
  
Adicionar:{width:200, padding:8, backgroundColor:'Yellow', marginTop:20},

botões:{width:'25%', backgroundColor:'black', justifyContent:'center', alignItems:'center', height:'100%'},

header:{width:'100%',padding:20,backgroundColor:'#069'},

anotação:{fontSize:14},

botãoprincipal:{position:'absolute',right:20,bottom:20,width:50,height:50,backgroundColor:'#069',borderRadius:25},

oxdobotão:{color:'White',position:'relative',textAlign:'center',top:3,fontSize:30},

botãosalvo:{position:'absolute',right:20,bottom:20,width:50,paddingTop:10,paddingBottom:10,backgroundColor:'#069',borderRadius:10},

centeredView: {flex: 1,justifyContent: 'center',alignItems: 'center',marginTop: 22},

modalView: {margin: 20,backgroundColor: 'white',borderRadius: 20,padding: 35,alignItems: 'center',shadowColor: '#000',shadowOpacity: 0.25,shadowRadius: 4,elevation: 5},

shadowOffset: {width: 0,height: 2},

button: {borderRadius: 20,padding: 10,elevation: 2},

buttonOpen: {backgroundColor: '#F194FF'},

buttonClose: {backgroundColor: '#2196F3'},

textStyle: {color: 'white',fontWeight: 'bold',textAlign: 'center'},

modalText: {marginBottom: 15,textAlign: 'center'},
});
