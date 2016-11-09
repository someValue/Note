####show a custom UIMenuItem for a UITableViewCell

TableViewController

	- (void)viewDidLoad
	{
	    [super viewDidLoad];
	    
	    UIMenuItem *copyMenuItem = [[UIMenuItem alloc] initWithTitle:@"复制" action:@selector(selfCopy:)];
	    [[UIMenuController sharedMenuController] setMenuItems: @[copyMenuItem]];
	    [[UIMenuController sharedMenuController] update];
	}


	#pragma mark - Table view delegate
	
	- (BOOL)tableView:(UITableView *)tableView shouldShowMenuForRowAtIndexPath:(NSIndexPath *)indexPath
	{
	    return YES;
	}
	
	-(BOOL)tableView:(UITableView *)tableView canPerformAction:(SEL)action forRowAtIndexPath:(NSIndexPath *)indexPath withSender:(id)sender {
	    return NO;
	}
	
	- (void)tableView:(UITableView *)tableView performAction:(SEL)action forRowAtIndexPath:(NSIndexPath *)indexPath withSender:(id)sender {}
	
TableViewCell

	-(BOOL) canPerformAction:(SEL)action withSender:(id)sender {
	    return (action == @selector(selfCopy:));
	}
	
	-(void) selfCopy:(id)sender {
	    [UIPasteboard generalPasteboard].string = @"哈哈哈哈dd";
	}