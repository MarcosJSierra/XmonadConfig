# instalando xmonad

primero instalaremos lo que necesitamos
sudo pacman -S xmonad xomand-contrib xterm dmenu xmobar
luego de esto debemos crear la carpeta xmonad en home
mkdir ~/.xomnad
descargamos el archivo de configuración de https://wiki.haskell.org/Xmonad/Config_archive y lo copiamos a la carpeta que creamos
cp ~/Downloads/xmonad.hs ~/.xmonad/xmonad.hs
cambiar 

myTerminal      = "konsole"

myBorderWidth   = 2

myModMask       = mod4Mask

myStartupHook = do 
    spawnOnce "nitrogen --restore &"
    spawnOnce "compton &"

debemos instalar nitrogen y comton

sudo pacman -S nitrogen compton

para buscar nitrogen usaremos 
win + p 
nitrogen 

ya qui seleciconaremos la carpeta donde estaran los backgrounds. usamos el siguiente comando 
xrandr
luego seleccionaremos la resolucion 
xrandr -r 1920x1080

ahora configuraremos xmobar primero crearemos la carpeta

mkdir ~/.config/xmobar
cd ~/.config/xmobar
touch xmobarrc
ahora editaremos xmonad.hs

import XMonad.Util.Run


main = do
    xmproc <- swapPipe "xmobar -x 0 /home/marcos/.config/xmobar/xmobarrc"
    xmonad $ docks defaults

import XMonad
import Data.Monoid
import System.Exit
import XMonad.Util.Run
import XMonad.Util.SpawnOnce
import XMonad.Hooks.ManageDocks


myLayout = avoidStruts (tiled ||| Mirror tiled ||| Full)

otra cosa que necesitaremos instalar sera:
light

con esto podremos controlar la iluminaci'on de la pantalla luego de esto agregaremos dos keys dentro de xmonad.hs

import qualified  Graphics.X11.ExtraTypes.XF86 as XF86

myKeys =[
    , ((0  ,  XF86.xF86XK_MonBrightnessUp), spawn "light -A 10")
    
    , ((0, XF86.xF86XK_MonBrightnessDown), spawn "light -U 10")
    ]