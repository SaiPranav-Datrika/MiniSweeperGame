package com.example.minisweepergame

import android.app.AlertDialog
import android.content.Intent
import android.os.Bundle
import android.view.View
import android.widget.*
import androidx.appcompat.app.AppCompatActivity
import kotlin.random.Random

class GameActivityMedium: AppCompatActivity(),View.OnClickListener
{

    var btnid= arrayOf(R.id.imageButton1,	R.id.imageButton2,	R.id.imageButton3,	R.id.imageButton4,	R.id.imageButton5,	R.id.imageButton6,	R.id.imageButton7,	R.id.imageButton8,	R.id.imageButton9,	R.id.imageButton10,
        R.id.imageButton11,	R.id.imageButton12,	R.id.imageButton13,	R.id.imageButton14,	R.id.imageButton15,	R.id.imageButton16,	R.id.imageButton17,	R.id.imageButton18,	R.id.imageButton19,	R.id.imageButton20,
        R.id.imageButton21,	R.id.imageButton22,	R.id.imageButton23,	R.id.imageButton24,	R.id.imageButton25,	R.id.imageButton26,	R.id.imageButton27,	R.id.imageButton28,	R.id.imageButton29,	R.id.imageButton30,
        R.id.imageButton31,	R.id.imageButton32,	R.id.imageButton33,	R.id.imageButton34,	R.id.imageButton35,	R.id.imageButton36,	R.id.imageButton37,	R.id.imageButton38,	R.id.imageButton39,	R.id.imageButton40,
        R.id.imageButton41,	R.id.imageButton42,	R.id.imageButton43,	R.id.imageButton44,	R.id.imageButton45,	R.id.imageButton46,	R.id.imageButton47,	R.id.imageButton48,	R.id.imageButton49,	R.id.imageButton50,
        R.id.imageButton51,	R.id.imageButton52,	R.id.imageButton53,	R.id.imageButton54,	R.id.imageButton55,	R.id.imageButton56,	R.id.imageButton57,	R.id.imageButton58,	R.id.imageButton59,	R.id.imageButton60,
        R.id.imageButton61,	R.id.imageButton62,	R.id.imageButton63,	R.id.imageButton64,	R.id.imageButton65,	R.id.imageButton66,	R.id.imageButton67,	R.id.imageButton68,	R.id.imageButton69,	R.id.imageButton70,
        R.id.imageButton71,	R.id.imageButton72,	R.id.imageButton73,	R.id.imageButton74,	R.id.imageButton75,	R.id.imageButton76,	R.id.imageButton77,	R.id.imageButton78,	R.id.imageButton79,	R.id.imageButton80,
        R.id.imageButton81,	R.id.imageButton82,	R.id.imageButton83,	R.id.imageButton84,	R.id.imageButton85,	R.id.imageButton86,	R.id.imageButton87,	R.id.imageButton88,	R.id.imageButton89,	R.id.imageButton90,
        R.id.imageButton91,	R.id.imageButton92,	R.id.imageButton93,	R.id.imageButton94,	R.id.imageButton95,	R.id.imageButton96,	R.id.imageButton97,	R.id.imageButton98,	R.id.imageButton99,	R.id.imageButton100
        )
    lateinit var imgbtn:Array<ImageButton>
    lateinit var g: GridLayout
    lateinit var t1: TextView
    //var screen=Array(8){CharArray(8)}
    lateinit var t2: TextView
    var currentmoveindex:Int=0
    var start:Int=0
    var x:Int=10
    var l:Int=2
    var side:Int
    var Level:Int
    var mines:Int
    var movesleft:Int
    var flagcount:Int=35
    // movesleft=(side*side)-mines
    var gameplay:Boolean=false
    var flagloc= mutableMapOf<String,Array<Int>>()

    var mineboard:Array<CharArray>
    var screenboard:Array<CharArray>
    var mineloc= mutableMapOf<String,Array<Int>>()
    var mark:Array<Boolean>


    init{
        side=x
        mines=(x*x/4)
        Level=l
        movesleft=(side*side)-mines
        mineboard=Array(side){ CharArray(side)}
        screenboard= Array(side){ CharArray(side) }
        mark=Array(side*side){false}}

    fun isValid(i:Int,j:Int,side:Int):Boolean{
        if(i>=0&&i<=side-1 && j<=side-1 && j>=0)
            return true
        return false
    }
    fun isMine(i:Int,j:Int,mineboard: Array<CharArray>):Boolean{
        if(mineboard[i][j]=='*')
            return true
        return false
    }
    fun initialize(mineboard:Array<CharArray>,screenboard:Array<CharArray>,side:Int){
        for(i in 0 until side)
            for(j in 0 until side)
            {
                mineboard[i][j]='-'
                screenboard[i][j]='-'
            }
    }
    fun placemines(mineboard: Array<CharArray>, side:Int, mines:Int){
        var i:Int=0
        while(i<=mines-1)
        {
            var random:Int= Random.nextInt(0,side*side)
            if(mark[random]==false){
                var x:Int=random/side
                var y:Int=random%side
                var init=arrayOf<Int>(2,x,y)
                var z:String=x.toString()+y.toString()
                mineloc.put(z,init)
                mineboard[x][y]='*'
                mark[random]=true
                i=i+1
            }


        }
    }
    fun replacemines(mineboard:Array<CharArray>,side:Int,row:Int,col:Int){
        var s:String=row.toString()+col.toString()
        mineloc.remove(s)
        for(i in 0..side-1){
            for(j in 0..side-1)
            {
                if(mineboard[i][j]=='-')
                {
                    mineboard[i][j]='*'
                    mineboard[row][col]='-'
                    mineloc.put(i.toString()+j.toString(), arrayOf(2,i,j))
                    return
                }
            }

        }
        return
    }
    fun count_mines(mineboard: Array<CharArray>, side: Int, screenboard:Array<CharArray>, i:Int, j:Int):Int{
        var count:Int=0
        for(x in i-1..i+1)
            for(y in j-1..j+1){
                if(x==i && y==j)
                    continue
                else if(isValid(x,y,side)==true ){
                    if(isMine(x,y,mineboard)==true)
                        count++
                }
            }
        return count
    }
    fun minisweepersetupafterclick(mineboard: Array<CharArray>, screenboard: Array<CharArray>, i:Int, j:Int, side:Int):Boolean{
        if(screenboard[i][j]!='-')
            return false

        if(mineboard[i][j]=='*'){
            for(key in mineloc.keys) {
                var s: String = key
                var x: Int = key[0].digitToInt()
                var y: Int =key[1].digitToInt()
                screenboard[x][y]='*'
            }
            screenboard[i][j]='*'

            flagcorrections()
            Toast.makeText(getApplicationContext(), "You Lost the Game", Toast.LENGTH_LONG).show()
            printboard(screenboard,true)


            return true
        }
        else{
            var count:Int
            var k:Int
            count=count_mines(mineboard,side,screenboard,i,j)
            k=count+48
            movesleft--

            screenboard[i][j]=(k.toChar())

            if(count==0) {
                for (x in i - 1..i + 1){
                    for (y in j - 1..j + 1) {
                        if (isValid(x, y, side) == true) {
                            if (isMine(x, y, mineboard) == false)
                                minisweepersetupafterclick(mineboard, screenboard, x, y, side)

                        }
                    }
                }
            }
            return false
        }
    }

    fun flagcorrections(){
        for((key,value) in flagloc){
            if(mineloc.containsKey(key)==false){
                //replace flag with XXXXX
                var s: String = key
                var x: Int = key[0].digitToInt()
                var y: Int =key[1].digitToInt()
                screenboard[x][y]='X'
            }
        }
    }
    fun flagcorrect():Boolean{
        var cnt:Int=0
        for((key,value) in flagloc){
            if(mineloc.containsKey(key)==true){
                cnt=cnt+1
            }
        }
        if(cnt+1==mines)
            return true

        return false
    }
    fun PlayMinisweepergame(i:Int,j:Int){
        //Toast.makeText(getApplicationContext(), i.toString()+j.toString(), Toast.LENGTH_LONG).show()
        if(start==0)
        {initialize(mineboard,screenboard,side)
            placemines(mineboard,side,mines)}
        start=1


        //while(gameplay==false) {
        //printboard
        //  gd.printboard(screenboard)
        //need to take the button click value from Mainactivity

        var row: Int=i
        var col: Int=j
        if(mineboard[row][col]=='*' && currentmoveindex==0){
            replacemines(mineboard,side,row,col)
        }
        currentmoveindex++

        gameplay = minisweepersetupafterclick(mineboard, screenboard, row, col, side)

        if (gameplay == false && movesleft == 0) {
            //Won the Game
            //flag corrections too
            //print the board
            Toast.makeText(getApplicationContext(),"You Won The Game", Toast.LENGTH_LONG).show()
            printboard(screenboard,false)
            gameplay=true
            return
            //  gameplay=true
        }

        // }
        if(gameplay==false)
            printboard(screenboard,false)

    }
    fun flag_insert_removal(i:Int,j:Int){
        if(screenboard[i][j]=='-') {
            movesleft=movesleft-1
            flagcount=flagcount-1
            screenboard[i][j]='F'
            flagloc.put(i.toString()+j.toString(), arrayOf(2,i,j))
        }
        else
            screenboard[i][j]='-'

        printboard(screenboard,false)
    }

    fun printboard(screenboard:Array<CharArray>,b:Boolean){
        // Toast.makeText(getApplicationContext(), "You Lost the Game", Toast.LENGTH_LONG)

        var m:Int=0
        for(i in 0..9){
            for(j in 0..9){
                m++

                if(screenboard[i][j]=='*' && b==true)
                {
                    imgbtn[m-1].setImageResource(R.mipmap.bomb2_round)
                }
                else if(screenboard[i][j]=='X' && b==true)
                {
                    imgbtn[m-1].setImageResource(R.drawable.clear)
                }
                else if(screenboard[i][j]=='F'){
                    imgbtn[m-1].setImageResource(R.drawable.flags)
                }
                else if(screenboard[i][j]=='0')
                    imgbtn[m-1].setImageResource(R.drawable.bike)
                else if(screenboard[i][j]=='1'){
                    imgbtn[m-1].setImageResource(R.drawable.ic_baseline_looks_one_24)
                }
                else if(screenboard[i][j]=='2'){
                    imgbtn[m-1].setImageResource(R.drawable.ic_baseline_looks_two_24)
                }
                else if(screenboard[i][j]=='3'){
                    imgbtn[m-1].setImageResource(R.drawable.vectorthree)
                }
                else if(screenboard[i][j]=='4'){
                    imgbtn[m-1].setImageResource(R.drawable.vectorfour)
                }
                else if(screenboard[i][j]=='5'){
                    imgbtn[m-1].setImageResource(R.drawable.vectorfive)
                }
                else if(screenboard[i][j]=='6'){
                    imgbtn[m-1].setImageResource(R.drawable.vectorsix)
                }
                else if(screenboard[i][j]=='7'){
                    imgbtn[m-1].setImageResource(R.drawable.vectorseven)
                }
                else if(screenboard[i][j]=='8'){
                    imgbtn[m-1].setImageResource(R.drawable.vectoreight)
                }

            }
            //  k=8
        }
    }

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.gamesetupmedium)
        var intent: Intent = getIntent()
        var s: String? =intent.getStringExtra("Key")

        imgbtn= arrayOf(
            findViewById(btnid[0]),	findViewById(btnid[1]),	findViewById(btnid[2]),	findViewById(btnid[3]),	findViewById(btnid[4]),	findViewById(btnid[5]),	findViewById(btnid[6]),	findViewById(btnid[7]),	findViewById(btnid[8]),	findViewById(btnid[9]),findViewById(btnid[10]),
            findViewById(btnid[11]),findViewById(btnid[12]),findViewById(btnid[13]),findViewById(btnid[14]),	findViewById(btnid[15]),	findViewById(btnid[16]),	findViewById(btnid[17]),	findViewById(btnid[18]),	findViewById(btnid[19]), findViewById(btnid[20]),
            findViewById(btnid[21]),findViewById(btnid[22]),findViewById(btnid[23]),	findViewById(btnid[24]),	findViewById(btnid[25]),	findViewById(btnid[26]),	findViewById(btnid[27]),	findViewById(btnid[28]),	findViewById(btnid[29]), findViewById(btnid[30]),
            findViewById(btnid[31]),findViewById(btnid[32]),	findViewById(btnid[33]),	findViewById(btnid[34]),	findViewById(btnid[35]),	findViewById(btnid[36]),	findViewById(btnid[37]),	findViewById(btnid[38]),	findViewById(btnid[39]), findViewById(btnid[40]),
            findViewById(btnid[41]),	findViewById(btnid[42]),	findViewById(btnid[43]),	findViewById(btnid[44]),	findViewById(btnid[45]),	findViewById(btnid[46]),	findViewById(btnid[47]),	findViewById(btnid[48]),	findViewById(btnid[49]), findViewById(btnid[50]),
            findViewById(btnid[51]),	findViewById(btnid[52]),	findViewById(btnid[53]),	findViewById(btnid[54]),	findViewById(btnid[55]),	findViewById(btnid[56]),	findViewById(btnid[57]),	findViewById(btnid[58]),	findViewById(btnid[59]), findViewById(btnid[60]),
            findViewById(btnid[61]),	findViewById(btnid[62]),	findViewById(btnid[63]),	findViewById(btnid[64]),	findViewById(btnid[65]),	findViewById(btnid[66]),	findViewById(btnid[67]),	findViewById(btnid[68]),	findViewById(btnid[69]), findViewById(btnid[70]),
            findViewById(btnid[71]),	findViewById(btnid[72]),	findViewById(btnid[73]),	findViewById(btnid[74]),	findViewById(btnid[75]),	findViewById(btnid[76]),	findViewById(btnid[77]),	findViewById(btnid[78]),	findViewById(btnid[79]), findViewById(btnid[80]),
            findViewById(btnid[81]),	findViewById(btnid[82]),	findViewById(btnid[83]),	findViewById(btnid[84]),	findViewById(btnid[85]),	findViewById(btnid[86]),	findViewById(btnid[87]),	findViewById(btnid[88]),	findViewById(btnid[89]), findViewById(btnid[90]),
            findViewById(btnid[91]),	findViewById(btnid[92]),	findViewById(btnid[93]),	findViewById(btnid[94]),	findViewById(btnid[95]),	findViewById(btnid[96]),	findViewById(btnid[97]),	findViewById(btnid[98]),	findViewById(btnid[99])
        )

        t1=findViewById(R.id.flag_count)
        t2=findViewById(R.id.textView4)
        imgbtn[0].setOnClickListener(this)
        imgbtn[1].setOnClickListener(this)
        imgbtn[2].setOnClickListener(this)
        imgbtn[3].setOnClickListener(this)
        imgbtn[4].setOnClickListener(this)
        imgbtn[5].setOnClickListener(this)
        imgbtn[6].setOnClickListener(this)
        imgbtn[7].setOnClickListener(this)
        imgbtn[8].setOnClickListener(this)
        imgbtn[9].setOnClickListener(this)
        imgbtn[10].setOnClickListener(this)
        imgbtn[11].setOnClickListener(this)
        imgbtn[12].setOnClickListener(this)
        imgbtn[13].setOnClickListener(this)
        imgbtn[14].setOnClickListener(this)
        imgbtn[15].setOnClickListener(this)
        imgbtn[16].setOnClickListener(this)
        imgbtn[17].setOnClickListener(this)
        imgbtn[18].setOnClickListener(this)
        imgbtn[19].setOnClickListener(this)
        imgbtn[20].setOnClickListener(this)
        imgbtn[21].setOnClickListener(this)
        imgbtn[22].setOnClickListener(this)
        imgbtn[23].setOnClickListener(this)
        imgbtn[24].setOnClickListener(this)
        imgbtn[25].setOnClickListener(this)
        imgbtn[26].setOnClickListener(this)
        imgbtn[27].setOnClickListener(this)
        imgbtn[28].setOnClickListener(this)
        imgbtn[29].setOnClickListener(this)
        imgbtn[30].setOnClickListener(this)
        imgbtn[31].setOnClickListener(this)
        imgbtn[32].setOnClickListener(this)
        imgbtn[33].setOnClickListener(this)
        imgbtn[34].setOnClickListener(this)
        imgbtn[35].setOnClickListener(this)
        imgbtn[36].setOnClickListener(this)
        imgbtn[37].setOnClickListener(this)
        imgbtn[38].setOnClickListener(this)
        imgbtn[39].setOnClickListener(this)
        imgbtn[40].setOnClickListener(this)
       imgbtn[41].setOnClickListener(this)
        imgbtn[42].setOnClickListener(this)
        imgbtn[43].setOnClickListener(this)
        imgbtn[44].setOnClickListener(this)
        imgbtn[45].setOnClickListener(this)
        imgbtn[46].setOnClickListener(this)
        imgbtn[47].setOnClickListener(this)
        imgbtn[48].setOnClickListener(this)
        imgbtn[49].setOnClickListener(this)
        imgbtn[50].setOnClickListener(this)
        imgbtn[51].setOnClickListener(this)
        imgbtn[52].setOnClickListener(this)
        imgbtn[53].setOnClickListener(this)
        imgbtn[54].setOnClickListener(this)
        imgbtn[55].setOnClickListener(this)
        imgbtn[56].setOnClickListener(this)
        imgbtn[57].setOnClickListener(this)
        imgbtn[58].setOnClickListener(this)
        imgbtn[59].setOnClickListener(this)
        imgbtn[60].setOnClickListener(this)
        imgbtn[61].setOnClickListener(this)
        imgbtn[62].setOnClickListener(this)
        imgbtn[63].setOnClickListener(this)
        imgbtn[64].setOnClickListener(this)
        imgbtn[65].setOnClickListener(this)
        imgbtn[66].setOnClickListener(this)
        imgbtn[67].setOnClickListener(this)
        imgbtn[68].setOnClickListener(this)
        imgbtn[69].setOnClickListener(this)
        imgbtn[70].setOnClickListener(this)
        imgbtn[71].setOnClickListener(this)
        imgbtn[72].setOnClickListener(this)
        imgbtn[73].setOnClickListener(this)
        imgbtn[74].setOnClickListener(this)
        imgbtn[75].setOnClickListener(this)
        imgbtn[76].setOnClickListener(this)
        imgbtn[77].setOnClickListener(this)
        imgbtn[78].setOnClickListener(this)
        imgbtn[79].setOnClickListener(this)
        imgbtn[80].setOnClickListener(this)
        imgbtn[81].setOnClickListener(this)
        imgbtn[82].setOnClickListener(this)
        imgbtn[83].setOnClickListener(this)
        imgbtn[84].setOnClickListener(this)
        imgbtn[85].setOnClickListener(this)
        imgbtn[86].setOnClickListener(this)
        imgbtn[87].setOnClickListener(this)
        imgbtn[88].setOnClickListener(this)
        imgbtn[89].setOnClickListener(this)
        imgbtn[90].setOnClickListener(this)
        imgbtn[91].setOnClickListener(this)
        imgbtn[92].setOnClickListener(this)
        imgbtn[93].setOnClickListener(this)
        imgbtn[94].setOnClickListener(this)
        imgbtn[95].setOnClickListener(this)
        imgbtn[96].setOnClickListener(this)
        imgbtn[97].setOnClickListener(this)
        imgbtn[98].setOnClickListener(this)
        imgbtn[99].setOnClickListener(this)

    }



    override fun onClick(v: View?) {
        var a: AlertDialog.Builder= AlertDialog.Builder(this)
        var mview:View=layoutInflater.inflate(R.layout.dialogbox,null)
        var b1:ImageButton=mview.findViewById(R.id.placeflag)
        var b2:ImageButton=mview.findViewById(R.id.dig)
        var b3:ImageButton=mview.findViewById(R.id.Cancel)
        a.setView(mview)
        var alertdialog: AlertDialog =a.create()
        alertdialog.setCanceledOnTouchOutside(false)
        b3.setOnClickListener {
            alertdialog.dismiss()
        }
        b1.setOnClickListener {
            for(i in 0..99) {
                if (v!!.id == btnid[i]) {
                    g = imgbtn[i].parent as GridLayout
                    var r: Int = g.indexOfChild(imgbtn[i]) / g.columnCount
                    var c: Int = g.indexOfChild(imgbtn[i]) % g.rowCount
                    flag_insert_removal(r,c)
                    break
                }
            }
            t1.text=flagcount.toString()
            if(flagcorrect())
            { Toast.makeText(getApplicationContext(),"You Won The Game",Toast.LENGTH_LONG).show()
                printboard(screenboard,false)
                gameplay=true}
            alertdialog.dismiss()
        }
        b2.setOnClickListener {

            if(gameplay==false){
                for(i in 0..99){
                    if(v!!.id==btnid[i]){
                        g = imgbtn[i].parent as GridLayout
                        var r: Int = g.indexOfChild(imgbtn[i]) / g.columnCount
                        var c: Int = g.indexOfChild(imgbtn[i]) % g.rowCount
                        //  Toast.makeText(getApplicationContext(), r.toString()+c.toString(), Toast.LENGTH_LONG).show()

                        PlayMinisweepergame(r,c)
                        //  printboard(screenboard,false)
                        break
                    }
                }
                t1.text=flagcount.toString()
                t2.text=movesleft.toString()
            }
            else
            { var bt: Button =findViewById(v!!.id)
                bt.setEnabled(false)
            }
            alertdialog.dismiss()
        }
        alertdialog.show()
    }
}
