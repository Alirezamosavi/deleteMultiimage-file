
add the below code in controller

  public function delete_user($id)
    {
       $single_user_id = explode(',' , $id);          //  by this code we get each id that is request to delete
      

 

        foreach ($single_user_id as $id) {  // by this function we can get one by one id 
           $i = uploadimage::findOrFail($id);  // in here we get all id that request from user
           $i->delete();
           $currentPhoto = $i->photo;  // by this code i can find all photo that get from database so according that i can find photo in public/img folder

           $userPhoto = public_path('img/public/').$currentPhoto; 

           if(file_exists($userPhoto)) {  // if exist image or fil in public/img then....

            @unlink($userPhoto);  // delete or move image from public/img
              
      }

        }
        
        return ['message' => 'deleted successfully'];

    }
	
write a router to that in api
Route::post('store_image/delete/{id}', 'App\Http\Controllers\PhotoController@delete_user');	

this is url to delete multi data
http://localhost:8000/api/store_image/delete/{id}	
	
