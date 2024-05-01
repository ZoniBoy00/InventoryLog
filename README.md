# ox_inventory log
------------------------------------------------------------------------

ox_lib > imports > logger

if service == 'discord' then
    local webhook = GetConvar('inventory:webhook', '')

    function lib.logger(source, event, message, ...)
        PerformHttpRequest(webhook, function() end, 'POST', json.encode({
            username = cache.resource,
            embeds = {
                {
                    ['title'] = 'action: ' .. event or 'UNKNOWN EVENT' .. ' by source: ' .. source or 'UNKNOWN SOURCE' .. ' (' .. GetPlayerName(source) or 'UNKNOWN PLAYER NAME' .. ')',
                    ['footer'] = {
                        ['text'] = os.date('%c'),
                    },
                    ['description'] = message or 'UNKNOWN MESSAGE'
                }
            }
        }), { ['Content-Type'] = 'application/json' })
    end
end
------------------------------------------------------------------------
Server.cfg

set inventory:webhook "WEBHOOK"
set ox:logger "discord"
------------------------------------------------------------------------
