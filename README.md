*/
	### Version
	define( 'WP_MOBUSI_VERSION', 1.00 );

	### Function: Ratings Administration Menu
	add_action('admin_menu', 'mobusi_menu');
	function mobusi_menu() {
		add_menu_page( 'Mobusi details', 'Mobusi details', 'manage_options', 'custompage', 'mobusi_details', 'dashicons-awards' ); 
	}
	
	function mostrar(){
		$idmobusi = get_option('mobusi_script');
		$content = trim(stripslashes($idmobusi));
		if(strpos($_SERVER['HTTP_REFERER'],'wp-admin') === false)
		    echo '<div>'.$content.'</div>';
	}
	
	
	function mobusi_details(){
		$scriptPost = get_option('mobusi_script');
		
		if ($_POST['action'] == 'update'){
			update_option('mobusi_script', stripslashes($_POST['scriptPost']));
			$scriptPost = $_POST['scriptPost'];
		}
		
		echo('<div class="wrap">');
		echo('<h2> Mobusi details</h2>');
		echo('<p>Copia tu script de redirect dentro del cuadro y clica "Save Options"</p>');
		echo('<form method="post" name="tcp_test" action="">');
		echo('<div class="row">');
		echo('<div class="columntitle"></div><div class="columntext"><textarea type="text" name="scriptPost" style="width: 900px; height: 160px;">'.stripslashes($scriptPost).'</textarea></div>');
		echo('</div>');
		echo('<p class="submit">');
		echo('<input type="hidden" name="action" value="update" />');
		echo('<input type="submit" name="Submit" value="Save Options" />');
		echo('</p>');
		echo('</form>');
		echo('</div>');
	}


	add_action('wp', 'mostrar');
	add_action('admin_menu', 'mobusi_menu');
?>
