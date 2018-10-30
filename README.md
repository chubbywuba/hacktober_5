# hacktober_5
random
#Tmux should be pretty, we need 256 color for that
set-option -ga terminal-overrides ",xterm-256color:Tc"

run-shell "powerline-daemon -q"
source "/usr/lib/python3.6/site-packages/powerline/bindings/tmux/powerline.conf"

bind-key m set-option -g mouse on \; display 'Mouse: ON'
bind-key M set-option -g mouse off \; display 'Mouse: OFF'
bind-key u capture-pane \; save-buffer /tmp/tmux-buffer \; new-window -n "urlview" '$SHELL -c "urlview < /tmp/tmux-buffer"'
#set Zsh as your default Tmux shell
set-option -g default-shell /bin/zsh

#Tmux uses a 'control key', let's set it to 'Ctrl-a'
#Reason: 'Ctrl-a' is easier to reach than 'Ctrl-b'
set -g prefix C-a
unbind C-b

#command delay? We don't want that, make it short
set -sg escape-time 1


set -g status on
setw -q -g utf8 on

set -s focus-events on

set -g set-titles on


setw -g automatic-rename on  # rename window to reflect current program
set -g renumber-windows on   # renumber windows when a window is closed
set -g status-interval 1     # redraw status line every 1 seconds

#activity
set -g monitor-activity on
set -g visual-activity off

#pane navigation
bind -r h select-pane -L  # move left
bind -r j select-pane -D  # move down
bind -r k select-pane -U  # move up
bind -r l select-pane -R  # move right
bind > swap-pane -D       # swap current pane with the next one
bind < swap-pane -U # swap current pane with the previous one

#pane resizing
bind -r H resize-pane -L 2
bind -r J resize-pane -D 2
bind -r K resize-pane -U 2
bind -r L resize-pane -R 2

#window navigation
unbind n
unbind p
bind -r C-h previous-window # select previous window
bind -r C-l next-window     # select next window
bind Tab last-window # move to last active window

#-- copy mode -----------------------------------------------------------------

bind Enter copy-mode # enter copy mode
bind b list-buffers  # list paster buffers
bind p paste-buffer  # paste from the top pate buffer
bind P choose-buffer # choose which buffer to paste from

#the following vi-copy bindings match my vim settings
#see https://github.com/gpakosz/.vim.git
bind -t vi-copy v begin-selection
bind -t vi-copy C-v rectangle-toggle
bind -t vi-copy y copy-selection
bind -t vi-copy Escape cancel
bind -t vi-copy H start-of-line
bind -t vi-copy L end-of-line




#Allow us to reload our Tmux configuration while
#using Tmux
bind r source-file ~/.tmux.conf \; display "Reloaded .tmux.conf!"

#Getting interesting now, we use the vertical and horizontal
#symbols to split the screen
bind | split-window -h
bind - split-window -v

##COLORSCHEME: gruvbox dark
set-option -g status "on"


#default statusbar colors
set-option -g status-bg colour237 #bg1
set-option -g status-fg colour223 #fg1

#default window title colors
set-window-option -g window-status-bg colour214 #yellow
set-window-option -g window-status-fg colour237 #bg1

set-window-option -g window-status-activity-bg colour237 #bg1
set-window-option -g window-status-activity-fg colour248 #fg3

#active window title colors
set-window-option -g window-status-current-bg default
set-window-option -g window-status-current-fg colour237 #bg1

#pane border
set-option -g pane-active-border-fg colour250 #fg2
set-option -g pane-border-fg colour237 #bg1

#message infos
set-option -g message-bg colour239 #bg2
set-option -g message-fg colour223 #fg1

#writting commands inactive
set-option -g message-command-bg colour239 #fg3
set-option -g message-command-fg colour223 #bg1

#pane number display
set-option -g display-panes-active-colour colour250 #fg2
set-option -g display-panes-colour colour237 #bg1

#clock
set-window-option -g clock-mode-colour colour109 #blue

#bell
set-window-option -g window-status-bell-style fg=colour235,bg=colour167 #bg, red


##Theme settings mixed with colors (unfortunately, but there is no cleaner way)
set-option -g status-attr "none"
set-option -g status-justify "left"
set-option -g status-left-attr "none"
set-option -g status-left-length "80"
set-option -g status-right-attr "none"
set-option -g status-right-length "80"
set-window-option -g window-status-activity-attr "none"
set-window-option -g window-status-attr "none"
set-window-option -g window-status-separator ""

set-option -g status-left "#[fg=colour248, bg=colour241] #S #[fg=colour241, bg=colour237, nobold, noitalics, nounderscore]"
set-option -g status-right "#[fg=colour239, bg=colour237, nobold, nounderscore, noitalics]#[fg=colour246,bg=colour239] %Y-%m-%d  %H:%M #[fg=colour248, bg=colour239, nobold, noitalics, nounderscore]#[fg=colour237, bg=colour248] #h "

set-window-option -g window-status-current-format "#[fg=colour239, bg=colour248, :nobold, noitalics, nounderscore]#[fg=colour239, bg=colour214] #I #[fg=colour239, bg=colour214, bold] #W #[fg=colour214, bg=colour237, nobold, noitalics, nounderscore]"
set-window-option -g window-status-format "#[fg=colour237,bg=colour239,noitalics]#[fg=colour223,bg=colour239] #I #[fg=colour223, bg=colour239] #W #[fg=colour239, bg=colour237, noitalics]"
