# Zack Test


<?php
    echo "Zackpang ist der Coolste";
<?php

namespace FBar;

use pocketmine\plugin\PluginBase;
use pocketmine\event\Listener;
use pocketmine\utils\TextFormat as F;
use pocketmine\scheduler\CallbackTask;
use onebone\economyapi\EconomyAPI;
use _64FF00\PurePerms\PurePerms;
use pocketmine\Player;

class FBar extends PluginBase implements Listener{

public $eco;
public $pp;

  public function onEnable(){
   $this->getServer()->getPluginManager()->registerEvents($this, $this);
     $this->eco = $this->getServer()->getPluginManager()->getPlugin("EconomyAPI");
       $this->pp = $this->getServer()->getPluginManager()->getPlugin("PurePerms");
        $this->getServer()->getScheduler()->scheduleRepeatingTask(new CallbackTask(array($this, "onMyBar")), 20 * 1);
         $this->getLogger()->info(F::GREEN . "Плагин включен!");
}
  public function onDisable(){
   $this->getLogger()->info(F::RED . "Плагин выключен!");
}
  public function onMyBar(){
   foreach($this->getServer()->getOnlinePlayers() as $players){
    $money = $this->eco->myMoney($players);
   $group = $this->pp->getUserDataMgr()->getGroup($players)->getName();
   $name = $players->getName();
   $online = count($this->getServer()->getOnlinePlayers());
   $max = $this->getServer()->getMaxPlayers();
   $right = str_repeat(" ", 45);
     $players->sendTip("".$right."§l§b•§r§f Ник:§e ".$name."\n".$right."§l§b•§r §fПривилегия:§e ".$group."\n".$right."§l§b•§r §fБаланс:§e ".$money."$\n".$right."§l§b•§r §fОнлайн:§e ".$online."/".$max." ");
    }
   }
  }
?>
