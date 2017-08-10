# GadgetEventEx

GadgetEventEx-Module for SpiderBasic

SpiderBasic unterstützt (aus Kompatibilitätsgründen zu PureBasic) relativ wenig Gadget-Ereignisse. So feuert beispielsweise das TextGadget überhaupt keine und das StringGadget nur drei Events (`#PB_EventType_Change`, `#PB_EventType_Focus` und `#PB_EventType_LostFocus`).

Mit dem GadgetEventEx-Modul ist es möglich, alle in JavaScript verfügbaren Ereignisse einem Gadget zuzuordnen.

## Code-Beispiel:
```
XIncludeFile "GadgetEventEx.sbi"

EnableExplicit

Enumeration
  #Window
  #StringGadget
  #TextGadget
  #ButtonGadget
EndEnumeration

Procedure HandleGadgetEventEx(e)
  
  Select EventGadget()
    Case #StringGadget
      Debug "Event from #StringGadget"
    Case #TextGadget
      Debug "Event from #TextGadget"
    Case #ButtonGadget
      Debug "Event from #ButtonGadget"
    Default
      Debug "Event from ???"
  EndSelect
  
  Debug "EventGadget(): " + EventGadget()
  Debug "EventTypeEx(): " + GadgetEventEx::EventTypeEx()
  Debug "-----"
  
EndProcedure


OpenWindow(#Window, 0, 0, 300, 300, "GadgetEventExDemo", #PB_Window_SystemMenu | #PB_Window_ScreenCentered)

; -------------------

StringGadget(#StringGadget, 10, 10, 100, 20, "StringGadget")

; bind all possible events for a StringGadget:

GadgetEventEx::Bind(#StringGadget, @HandleGadgetEventEx()) 

; -------------------

TextGadget(#TextGadget, 10, 50, 100, 20, "TextGadget")

; bind all possible events for a TextGadget (you can also use #PB_EventTypeEx_All):

GadgetEventEx::Bind(#TextGadget, @HandleGadgetEventEx(), GadgetEventEx::#PB_EventTypeEx_All)

; unbind MouseMove- and PointerMove-Events:

GadgetEventEx::Unbind(#TextGadget, @HandleGadgetEventEx(), GadgetEventEx::#PB_EventTypeEx_Mousemove + "|" + GadgetEventEx::#PB_EventTypeEx_Pointermove)

; -------------------

ButtonGadget(#ButtonGadget, 10, 80, 100, 25, "ButtonGadget")

; bind left- and right-click events for the ButtonGadget:

GadgetEventEx::Bind(#ButtonGadget, @HandleGadgetEventEx(), GadgetEventEx::#PB_EventTypeEx_Click + "|" + GadgetEventEx::#PB_EventTypeEx_Contextmenu)
```

## Lizenz

[MIT](https://github.com/spiderbytes/GadgetEventEx/blob/master/LICENSE)
