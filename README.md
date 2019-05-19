# THZ - Treasure Hunter Z
Created by @kts_kettek in response to @eigenbom, THZ is a treasure huntin' "rogue-like" game intended to fit in a single 140 character Tweet. It runs in the browser's developer console.

And what is the objective? To find the buried gold of a forgotten civilization (and maybe reload the page if you can't ;])

Check out the 560 character sequel [here](https://github.com/kettek/THZ-II/)!

## Code (paste in browser console)
    z=43;r=new Date%z;onkeyup=function(e){d=1-e.which%4;z+=d%2?d*9:-d-1;m='';for(a=1;a++<53;m+=a%9?a==z?a==r?'$':'@':'.':'\n');console.log(m)}

## Code Breakdown
    // player's start position
    z = 43;
    // randomized gold position, limited to player's start position
    r = new Date%z;
    
    // run game loop on each key press
    onkeyup = function(e) {
      /* Given that e.which returns the keycode, we modulo 4 it to get 4
      possible values. We negate this value ( 1 - X ) to save a couple
      characters in calculating the change in player position (z) - this
      results in up=-1, right=-2, left=0, down=1 */
      d = 1-e.which%4;
      /* Modify the player's position based on key press. By using
      modulo 2 on 'd', our up and down directions become -1 and 1 and our
      left and right become 0 and -0. -1 and 1 then evaluate to true, from
      which we can simply multiply 'd' by 9 and add that resulting value to
      our player position. Since 9 is the width of the map, this moves our
      player up or down. If the expression returns false, we simply negate d
      and subtract 1 - this returns -1 for left and 1 for right, which can
      then be added to the player's position. */
      z += d%2?d*9:-d-1;
      // Map generation
      m='';
      /* Here we build the map string. Every step from 1 to 53, we add a
      character to the 'm' string. 'a' represents our current tile position
      and simply draws a different tile depending on various conditions.
      These conditions are: if 'a' == 'r', then '$'; if 'a' == 'z', then '@';
      if 'a%9' != 0, then '.'; otherwise line break. */
      for (a=1;a++<53;m+=a%9?a==z?a==r?'$':'@':'.':'\n');
      // Draw map
      console.log(m)
    }

## Code rewrite
    // player's start position
    player = 43;
    // randomized gold position, limited to player's start position
    gold = new Date%player;
    
    // run game loop on each key press
    onkeyup = function(e) {
      /* Given that e.which returns the keycode, we modulo 4 it to get 4
      possible values. We negate this value ( 1 - X ) to save a couple
      characters in calculating the change in player position - this results
      in up=-1, right=-2, left=0, down=1 */
      d = 1-e.which%4;
      // Modify the player's position based on key press.
      if (d%2) { // is 'd' -1 or 1? If so, multiply by 9 to move our player up or down
        player += d * 9;
      } else { // otherwise negate d and subtract 1 and add the resulting value to our player (-1 for left, 1 for right)
        player += -d - 1;
      }
      // Map generation
      map = '';
      // Here we build the map string.
      for (tile = 0; tile < 53; tile++) {
        if (tile % 9) {
          if (tile == player) {
            if (tile == gold) {
              map += '$';
            } else {
              map += '@';
            }
          } else {
            map += '.';
          }
        } else {
          map += '\n';
        }
      }
      // Draw map
      console.log(map)
    }
