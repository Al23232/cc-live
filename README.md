#include
<stdio.h>
int main()
{printf("Hello world!");
return 0;
}Uncloset.
template literal
  utf.-(8)-_software__=
  CCchecker :" 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"
{}author__ =
 Handrix handrix@users.sourceforge.org" 
{}version__ = "1.0.1" 
{}cvsversion__ = "$Revision: 1.0 $" 
{}date__ = "$Date: 2006/12/25 23:46:07 $" pp
_copyright__ = "Copyright (c) 2006 Mark Handrix" 
__license__="GPL" 
__credits__ = "Thanks  securfox for support" 
""" 
 
import wx 
 
class Checkcard: 
    """Class Checkcard Checks for valid credit card number using Luhn algorithm.""" 
    """Defaulf constructor """ 
    def __init__(self): 
        self.bank = "" 
        self.number = "" 
        self.error = "" 
 
    def __set_number__(self, number): 
        if str(self.number).find(' '): 
            self.number = str(number).replace(' ','') 
        else: 
            self.number = number 
         
    def __get__number__(self): 
        return int(self.number) 
 
    def __set_bank__(self, bank): 
        self.bank = str(bank) 
 
    def __get_bank__(self): 
        return self.bank 
 
    def __ibank__(self): 
        """The first 6 digits of your credit card number (including the initial MII digit) form the issuer identifier. 
            So, this function return the issuer.""" 
        if len(str(self.number)) < 17 and len(str(self.number)) > 12 : 
            if str(self.number)[:2]=='34' or str(self.number)[:2]=='37' : 
               self.__set_bank__("AMEX") 
            elif str(self.number)[0]=='4': 
               self.__set_bank__("VISA") 
            elif int(str(self.number)[:2]) > 50 and int(str(self.number)[:2]) < 52: 
               self.__set_bank__("MASTERCARD") 
            elif str(self.number)[:4]=='6011': 
               self.__set_bank__("DISCOVER") 
            elif str(self.number)[:2]=='37' or str(self.number)[:2]=='38': 
               self.__set_bank__("CARTE BLANCHE") 
            elif int(str(self.number)[:3]) > 299 and int(str(self.number)[:3]) < 306: 
               self.__set_bank__("CARTE BLANCE NOT NULL ") 
            else: 
                self.error=(1) 
             
        else: 
            self.error=() 
 
    def __isvalid__(self): 
        """The final digit of a credit card number is a check digit, akin to a checksum. The algorithm used to arrive 
           at the proper check digit is called the Luhn algorithm. 
           fucntion __isvalid__ do this algorithm and return True if the algorithm success mean that is a valid card, 
           else we return TRUE """ 
 
        try: 
                temp, some = [], 0 
                for i in range(0,len(self.number)): 
                        temp.append(str(self.number)[i]) 
                        if i % 2 == 0: 
                           temp[i] = int(str(self.number)[i]) * 2 
                        if int(temp[i]) > 9: 
                            temp[i]=int(str(temp[i])[0]) + int(str(temp[i])[1]) 
                        some +=int(temp[i]) 
                if some % 10 == 0: 
                       return True 
                elif some % 10 == 1: 
                       return False 
        except Exception, msg: 
            pass 
 
 
class InterFrame(wx.Frame): 
    """Main Frame holding the cc validator Panel.""" 
    def __init__(self, *args, **kwargs): 
        wx.Frame.__init__(self, *args, **kwargs) 
        ico="D:\marnic\lib\cc\img\icon.ico" 
        self.icon = wx.Icon(ico, wx.BITMAP_TYPE_ICO)  
        self.SetIcon(self.icon) 
        self.mainPanel = wx.Panel(self, -1)                       
        self.input = "" 
        self.text = "" 
         
         
 
        
 
    def SetButton(self, button=[]): 
        if len(button) != 0: 
            try: 
                for i in range(len(button)): 
                    item = wx.Button(self.mainPanel, -1, button[i][0], button[i][2]) 
                    item.SetBackgroundColour("black") 
                    item.SetForegroundColour("green") 
                    self.Bind(wx.EVT_BUTTON, button[i][1], item) 
            except: 
                pass  
 
 
 
 
    def SetIOput(self, text1="",bg="black",fg="green"): 
	self.input  = wx.TextCtrl(self.mainPanel, -1, text1, size=(230,20),pos=(60,75)) 
        for i in [self.input]: 
            i.SetBackgroundColour(bg) 
            i.SetForegroundColour(fg)            
 
 
 
 
     
        self.input.SetMaxLength(25) 
        helpicon="D:\marnic\lib\cc\img\logos.png" 
        imag = wx.Image(helpicon, wx.BITMAP_TYPE_ANY).ConvertToBitmap()       
        wx.StaticBitmap(self.mainPanel, id=-1, bitmap=imag, pos=(230, 0), size = (imag.GetWidth(), imag.GetHeight())) 
  
	 
 
        self.output  = wx.TextCtrl(self.mainPanel, -1, "", size=(230,20),pos=(60,105)) 
        self.output.DiscardEdits() 
        self.output.SetEditable(False) 
        self.output.SetBackgroundColour("black") 
        self.output.SetForegroundColour("yellow")    
 
        
        self.panell=wx.Panel(self.mainPanel, -1, size=(65,45), pos=(22,140)) 
        self.panell.SetBackgroundColour('red')         
 
        self.panel=wx.Panel(self.mainPanel, -1, size=(61,41), pos=(24,142)) 
        self.panel.SetBackgroundColour('gray')  
 
 
        self.panell1=wx.Panel(self.mainPanel, -1, size=(65,45), pos=(92,140)) 
        self.panell1.SetBackgroundColour('red')         
 
        self.panel1=wx.Panel(self.mainPanel, -1, size=(61,41), pos=(94,142)) 
        self.panel1.SetBackgroundColour('gray')  
 
 
        self.panell2=wx.Panel(self.mainPanel, -1, size=(65,45), pos=(162,140)) 
        self.panell2.SetBackgroundColour('red')         
 
        self.panel1=wx.Panel(self.mainPanel, -1, size=(61,41), pos=(164,142)) 
        self.panel1.SetBackgroundColour('gray')  
 
 
        self.panell3=wx.Panel(self.mainPanel, -1, size=(65,45), pos=(232,140)) 
        self.panell3.SetBackgroundColour('red')         
 
        self.panel3=wx.Panel(self.mainPanel, -1, size=(61,41), pos=(234,142)) 
        self.panel3.SetBackgroundColour('gray')  
 
 
        self.panell4=wx.Panel(self.mainPanel, -1, size=(65,45), pos=(302,140)) 
        self.panell4.SetBackgroundColour('red')         
 
        self.panel4=wx.Panel(self.mainPanel, -1, size=(61,41), pos=(304,142)) 
        self.panel4.SetBackgroundColour('gray')  
 
 
     
        helpicon="D:\marnic\lib\cc\img\savi.gif" 
        imag = wx.Image(helpicon, wx.BITMAP_TYPE_ANY).ConvertToBitmap() 
        wx.BitmapButton(self.mainPanel, id=-1, bitmap=imag, pos=(23, 141), size = (imag.GetWidth()+3, imag.GetHeight()+4)) 
        
        helpicon="D:\marnic\lib\cc\img\mastercard.gif" 
        imag = wx.Image(helpicon, wx.BITMAP_TYPE_ANY).ConvertToBitmap()       
        wx.StaticBitmap(self.mainPanel, id=-1, bitmap=imag, pos=(93, 141), size = (imag.GetWidth(), imag.GetHeight()+2)) 
 
        helpicon="D:\marnic\lib\cc\img\mx.gif" 
        imag = wx.Image(helpicon, wx.BITMAP_TYPE_ANY).ConvertToBitmap() 
        wx.StaticBitmap(self.mainPanel, id=-1, bitmap=imag, pos=(163, 141), size = (imag.GetWidth()+2, imag.GetHeight()+3)) 
 
        helpicon="D:\marnic\lib\cc\img\discover.gif" 
        imag = wx.Image(helpicon, wx.BITMAP_TYPE_ANY).ConvertToBitmap() 
        wx.StaticBitmap(self.mainPanel, id=-1, bitmap=imag, pos=(234, 141), size = (imag.GetWidth()+4, imag.GetHeight()+6)) 
 
        
        helpicon="D:\marnic\lib\cc\img\diners_club_card.gif" 
        imag = wx.Image(helpicon, wx.BITMAP_TYPE_ANY).ConvertToBitmap() 
        wx.StaticBitmap(self.mainPanel, id=-1, bitmap=imag, pos=(305, 142), size = (imag.GetWidth(), imag.GetHeight()+3)) 
	 
 
        self.mainPanel.Bind(wx.EVT_KEY_DOWN, self.OnKeyEnter) 
        self.mainPanel.SetFocus() 
         
    def Oncheck(self,event=None): 
 
        valid = 1 
        self.panell.SetBackgroundColour('red')         
        self.panell1.SetBackgroundColour('red')         
        self.panell2.SetBackgroundColour('red')         
        self.panell3.SetBackgroundColour('red')  
        self.panell4.SetBackgroundColour('red')         
        
        number = frame.OnInput() 
        card = Checkcard() 
        card.__set_number__(number) 
        card.__ibank__() 
        if card.error==1: 
            valid=0 
        bank=card.__get_bank__() 
        if card.__isvalid__() is not None and valid==1: 
           value = "Card is valid     " 
        else: 
           value = "Card is Not valid " 
 
            
        self.output.Clear() 
        self.output.AppendText(value) 
         
        if bank.upper() == "VISA": 
            self.panell.SetBackgroundColour('green') 
        elif bank.upper() == "MASTERCARD": 
            self.panell1.SetBackgroundColour('green') 
        elif bank.upper() == "AMEX": 
            self.panell2.SetBackgroundColour('green') 
        elif bank.upper() == "DISCOVER": 
            self.panell3.SetBackgroundColour('green') 
        elif bank.upper() == "CARTE BLANCHE": 
            self.panell4.SetBackgroundColour('green') 
                 
        self.Refresh()       
 
 
 
    def OnKeyEnter(self, event): 
        keycode = event.GetKeyCode() 
        if keycode == wx.WXK_ENTER: 
            self.Oncheck() 
        event.Skip() 
         
         
    def OnQuit(self, event=None): 
        """Exit application.""" 
        self.Close() 
         
 
    def OnHelp(self,event=None): 
	text="Card credit checker 2006" + "\n" + " LICENCE GPL " 
	dialog=wx.MessageDialog(self, text, "apropos ...", wx.ICON_INFORMATION|wx.STAY_ON_TOP) 
	dialog.ShowModal() 
	dialog.Destroy() 
 
		 
    def OnClear(self, event=None): 
        self.panell.SetBackgroundColour('red')         
        self.panell1.SetBackgroundColour('red')         
        self.panell2.SetBackgroundColour('red')         
        self.panell3.SetBackgroundColour('red')  
        self.panell4.SetBackgroundColour('red')  
	self.input.Clear() 
	self.text="" 
        self.output.Clear() 
       
        self.Refresh()          
  
     
    def OnInput(self): 
        value = self.input.GetValue() 
        if  value.strip() != '' and value is not None: 
            return value 
 
 
         
if __name__ == '__main__': 
 
   
    app = wx.PySimpleApp() 
    frame=InterFrame(None, id=-1, title="Card credit checker", pos=wx.DefaultPosition, size=(400, 290)) 
    frame.SetBackgroundColour(wx.BLACK) 
    frame.SetIOput(text1="Enter card's number") 
    frame.SetButton(button=[("Check ",frame.Oncheck,(300,75)),("Clear",frame.OnClear,(220,210)),("Quit",frame.OnQuit,(300,210))]) 
    frame.Centre()     
    frame.Show() 
    app.MainLoop() 
 {
<pk_live_51HyqQsLQtKUNH5HkwSpKi1h16FGFlCIWEw96ucNjt8GyRU3RFXKU60M8NcyyYTOxJDqwfwmg8146qZLw6ft5QINo00yTdvpMr5
